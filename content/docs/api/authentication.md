---
title: Authentication
type: docs
layout: api
aliases:
  - /docs/api
---

Authentication mechanism is already implemented in all our official client libraries. If you are implementing a new 
client library for an unsupported language, or you are just curious how it works then this page will help you.  

Each API Key consists of a pair of Key Id and Secret Key. A Key Id is always provided with each request to identify a 
caller. A Secret Key is used to sign that request. An account can have multiple API keys. Any key can be revoked if 
needed. Each key has an associated role (more on Authorization [here](/docs/api/authorization)).   

Every API request should have the following headers:

* `evrblk-api-key-id` - API Key Id
* `evrblk-signature` - A signature of a given request
* `evrblk-timestamp` - A timestamp of a given request (Unix time in seconds)

Timestamps are used to prevent [Replay Attacks](https://en.wikipedia.org/wiki/Replay_attack). Each request should be 
timestamped within `[now - 5 min; now + 5 min]` interval to allow for some clock drift.

There are several supported authentication mechanisms that go by names: __Alfa__, and __Bravo__. They use
different signing methods, vary in performance, and trust level. If new mechanisms appear in the future, or there is a 
need to fix something in existing ones, they will be created under new names and existing mechanisms will be kept 
untouched for backward compatibility.

## Alfa

This is the recommended signing mechanism for enterprises and very paranoid users.

Alfa is based on __secp256r1__ (aka NIST P-256) cryptographic signature algorithm. Public and private keys are PEM 
encoded and are generated by user. Only the public key is stored in the cloud. That means that user keys cannot be 
compromised in an unlikely event of a security breach. That also means that Secret Key cannot be restored if it has 
been lost.

On the client side:

```text
timestamp_bytes = int64_to_bytes(timestamp) // 8 bytes big endian of Unix timestamp
request_bytes = proto_marshall(request) // binary proto representation of a request 
data = timestamp_bytes + request_bytes
signature = p256_sign(private_key, data)
```

On the server side:

```text
timestamp_bytes = int64_to_bytes(timestamp) // 8 bytes big endian of Unix timestamp
request_bytes = proto_marshall(request) // binary proto representation of a request 
data = timestamp_bytes + request_bytes
result = p256_verify(public_key, data)
```

__TODO: how to generate and where are the sources__ 

```shell
# Generate ecdsa private key with explicit secp256r1 curve
openssl ecparam -name secp256r1 -genkey -noout -out secp256r1-key.pem
# <private key output>

# From the private key, generate a public key
openssl ec -in secp256r1-key.pem -pubout -out secp256r1-pub.pem
```

## Bravo

Bravo is based on a large random string as a secret. It is not sufficient for very paranoid users because the secret is 
stored in the cloud. Bravo signing mechanism is much faster and simpler than Alfa. Bravo keys are used in Everblack 
Console, a new short-lived Bravo API key is created on each user sign in, the secret is encrypted and stored in cookies. 
On every request Console decrypts the secret from cookies and uses it to call Everblack API.
 
Bravo secret is 512 random bytes encoded in Base64. The signature is `sha256` of a timestamp, a request, and a hashed
secret (`sha256` of a secret key and a date). Extra step of hashing the secret with a date allows safe caching on API
servers without leaking the real secret outside AuthN service boundaries.

On the client side:

```text
timestamp_bytes = int64_to_bytes(timestamp) // 8 bytes big endian of Unix timestamp
request_bytes = proto_marshall(request) // binary proto representation of a request
date = dateOf(timestamp)
date_bytes = format(date) // date in "YYYY-MM-DD" format
hashed_secret = sha256(secret, date_bytes)
data = timestamp_bytes + request_bytes
signature = hmac_sha256(hashed_secret, data)
```

On the server side:

```text
timestamp_bytes = int64_to_bytes(timestamp) // 8 bytes big endian of Unix timestamp
request_bytes = proto_marshall(request) // binary proto representation of a request
date = dateOf(timestamp)
date_bytes = format(date) // date in "YYYY-MM-DD" format
hashed_secret = sha256(secret + date)
data = timestamp_bytes + request_bytes
expected_signature = hmac_sha256(hashed_secret, data)
result = actual_signature == expected_signature
```

__TODO: how to generate and where are the sources__

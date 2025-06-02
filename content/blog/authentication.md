---
title: "Authentication"
description: "Everything you need to know about authentication"
date: 2023-05-30
draft: false
keywords: ["authn", "authentication", "API"]
params:
  author: "Stanislav Spiridonov"
---

__Authentication__ -
__Authorization__ -

Timestamps are used to prevent Replay Attacks. Each request should be timestamped within `[now - 5 min; now + 5 min]`
interval to allow for some clock drift.

Alfa is based on RSA PKCS #1 v1.5 cryptographic signature algorithm. Alfa Secret Key is 1024 bits RSA Private Key
packaged as PKCS #1 and encoded as Base64 string. Only corresponding RSA Public Key is stored in the cloud. That means
that users keys cannot be compromised even in an unlikely case of a security breach. That also means that Secret Key
cannot be restored if it has been lost. 



## SigV4

Uses region name, service name, method name: to distinguish between signatures for calls with the same values of
arguments (or empty calls, such as List*).



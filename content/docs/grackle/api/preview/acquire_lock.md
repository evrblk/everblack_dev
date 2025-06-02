---
title: AcquireLock
type: docs
layout: grackle
---

Tries to grab a lock.

A lock with a given name does not have to be created before use, it is automatically instantiated on the first 
acquiring.

To grab the lock exclusively for writing provide `write_lock=true`, to grab for reading provide `write_lock=false`.

It returns `success` which indicates whether the lock was indeed acquired or not. It also returns the current state of
the lock, so you can see who is holding it at the moment if your request was not successful.

Request:

```json
{
  "namespace_name": "UserObjects",
  "lock_name": "user_object_12345667890",
  "process_id": "host-123/thread-123456",
  "write_lock": true,
  "expires_at": 1695826539671432000
}
```

Response:

```json
{
  "lock": {
    "name": "user_object_12345667890",
    "state": "WRITE_LOCKED",
    "locked_at": 1695826239671432000,            
    "write_lock_holder": {
      "process_id": "host-123/thread-123456",
      "locked_at": 1695826239671432000,
      "expires_at": 1695826539671432000
    },
    "read_lock_holders": []
  },
  "success": true
}
```

__AcquireLockRequest__

| Parameter                | Type                  |                                   |
|--------------------------|-----------------------|-----------------------------------|
| namespace_name           | String                | Required, max 128 chars           |
| lock_name                | String                | Required, max 128 chars           |
| process_id               | String                | Required, max 128 chars           |
| write_lock               | Boolean               | Optional, default false           |
| expires_at               | Integer               | Required, timestamp in the future |

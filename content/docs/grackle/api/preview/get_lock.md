---
title: GetLock
type: docs
layout: grackle
---

Gets a lock.

It always returns something. If a lock is unlocked this will return it anyway.

Request:

```json
{
  "namespace_name": "UserObjects",
  "lock_name": "user_object_12345667890"
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
  }
}
```

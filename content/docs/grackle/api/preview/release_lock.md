---
title: ReleaseLock
type: docs
layout: grackle
---

Releases a lock.

A lock with a given name does not have to be created before use, nor it has to be locked before releasing. It always 
returns the current state of the lock, so you can see who is holding it at the moment.

Request:

```json
{
  "namespace_name": "UserObjects",
  "lock_name": "user_object_12345667890",
  "process_id": "host-123/thread-123456"
}
```

Response:

```json
{
  "lock": {
    "name": "user_object_12345667890",
    "state": "UNLOCKED",
    "locked_at": 0,            
    "write_lock_holder": {},
    "read_lock_holders": []
  }
}
```


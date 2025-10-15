---
title: AcquireSemaphore
type: docs
layout: grackle
---

Tries to grab a semaphore.

A semaphore with a given name has to be created before with `CreateSemaphore`.

It returns `success` which indicates whether the semaphore was indeed acquired or not. It also returns the current state
of the semaphore, so you can see who is holding it at the moment if your request was not successful.

There are never more `semaphore_holders` than `permits`.

Request:

```json
{
  "namespace_name": "third_parties",
  "semaphore_name": "partner_1",
  "process_id": "host-123/thread-123456",
  "expires_at": 1695826539671432000
}
```

Response:

```json
{
  "semaphore": {
    "name": "partner_1",
    "description": "Partner 1 API",
    "created_at": 1695826239671432000,            
    "updated_at": 1695826239671432000,
    "permits": 20,
    "semaphore_holders": [
      {
        "process_id": "host-123/thread-123456",
        "locked_at": 1695826239671432000,
        "expires_at": 1695826539671432000
      }
    ]
  },
  "success": true
}
```


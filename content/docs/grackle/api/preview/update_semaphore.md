---
title: UpdateSemaphore
type: docs
layout: grackle
---

Request:

```json
{
  "namespace_name": "third_parties",
  "semaphore_name": "partner_1",
  "description": "New Partner 1 API",
  "permits": 30
}
```

Response:

```json
{
  "semaphore": {
    "name": "partner_1",
    "description": "New Partner 1 API",
    "created_at": 1695826239671432000,            
    "updated_at": 1695826239925421000,
    "permits": 30,
    "semaphore_holders": [
      {
        "process_id": "host-123/thread-123456",
        "locked_at": 1695826239671432000,
        "expires_at": 1695826539671432000
      }
    ]
  }
}
```

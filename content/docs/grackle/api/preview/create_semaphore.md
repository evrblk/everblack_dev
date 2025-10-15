---
title: CreateSemaphore
type: docs
layout: grackle
---

Creates a semaphore.

Request:

```json
{
  "namespace_name": "third_parties",
  "semaphore_name": "partner_1",
  "description": "Partner 1 API",
  "permits": 20
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
    "semaphore_holders": []
  }
}
```

---
title: GetWaitGroup
type: docs
layout: grackle
---

Gets a wait group.

Request:

```json
{
  "namespace_name": "mynamespace",
  "wait_group_name": "wg_123"
}
```

Response:

```json
{
  "wait_group": {
    "name": "wg_123",
    "description": "description",
    "created_at": 1695826239671432000,
    "updated_at": 1695826239671432000,
    "expires_at": 1695826543671432000,
    "counter": 100,
    "completed": 12
  }
}
```

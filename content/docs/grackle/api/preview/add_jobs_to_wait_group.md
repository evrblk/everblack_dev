---
title: AddJobsToWaitGroup
type: docs
layout: grackle
---

Adds more jobs to a wait group's `counter`.

Request:

```json
{
  "namespace_name": "mynamespace",
  "wait_group_name": "wg_123",
  "counter": 10
}
```

Response:

```json
{
  "wait_group": {
    "name": "wg_123",
    "description": "description",
    "created_at": 1695826239671432000,
    "updated_at": 1695826239925421000,
    "expires_at": 1695826543671432000,
    "counter": 110,
    "completed": 12
  }
}
```

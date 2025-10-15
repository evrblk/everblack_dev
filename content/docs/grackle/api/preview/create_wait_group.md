---
title: CreateWaitGroup
type: docs
layout: grackle
---

Creates a wait group.

Wait groups have an expiration time after that they will be deleted regardless of whether they were completed or not.

You don't need to specify upfront all jobs IDs that will constitute this wait group, you only need to know the number
of those jobs (`counter`). That number can be millions.

Request:

```json
{
  "namespace_name": "my_namespace",
  "wait_group_name": "wg_123",
  "description": "description",
  "counter": 100,
  "expires_at": 1695826543671432000
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
    "completed": 0
  }
}
```

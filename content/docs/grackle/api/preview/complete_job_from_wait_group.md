---
title: CompleteJobFromWaitGroup
type: docs
layout: grackle
---

Marks a list of `process_ids` jobs as completed.

`completed` counter will be incremented if a process ID has not been reported before. Process IDs are unique within a
wait group, but do not have to be unique between multiple groups.

Request:

```json
{
  "namespace_name": "mynamespace",
  "wait_group_name": "wg_123",
  "process_ids": [
    "process_1", "process_2"
  ]
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
    "completed": 14
  }
}
```

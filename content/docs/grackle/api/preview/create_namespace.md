---
title: CreateNamespace
type: docs
layout: grackle
---

Creates a namespace.

Request:

```json
{
  "name": "UserObjects",
  "description": "Some description"
}
```

Response:

```json
{
  "namespace": {
    "name": "UserObjects",
    "description": "Some description",
    "created_at": 1695826239671432000,
    "updated_at": 1695826239671432000
  }
}
```

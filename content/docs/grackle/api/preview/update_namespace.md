---
title: UpdateNamespace
type: docs
layout: grackle
---

Request:

```json
{
  "namespace_name": "UserObjects",
  "description": "New description"
}
```

Response:

```json
{
  "namespace": {
    "name": "UserObjects",
    "description": "New description",
    "created_at": 1695826239671432000,
    "updated_at": 1695826239925421000
  }
}
```

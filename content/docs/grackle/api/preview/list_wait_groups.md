---
title: ListWaitGroups
type: docs
layout: grackle
---

Lists all wait groups in a given namespace. This is a paginated API. When `pagination_token` is empty it returns the first
page. Non-empty `next_pagination_token` and `previous_pagination_token` in the response indicate that there are other
pages available before or after the current page.

Request:

```json
{
  "namespace_name": "mynamespace",
  "pagination_token": "bXlsb25ndG9rZW4xCg==",
  "limit": 100
}
```

Response:

```json
{
  "wait_groups": [
    {
      "name": "wg_123",
      "description": "description",
      "created_at": 1695826239671432000,
      "updated_at": 1695826239671432000,
      "expires_at": 1695826543671432000,
      "counter": 100,
      "completed": 12
    }
  ],
  "next_pagination_token": "bXlsb25ndG9rZW4yCg==",
  "previous_pagination_token": "bXlsb25ndG9rZW4xCg=="
}
```

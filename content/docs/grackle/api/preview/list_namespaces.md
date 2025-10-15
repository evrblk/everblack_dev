---
title: ListNamespaces
type: docs
layout: grackle
---

Lists all namespaces. This is a paginated API. When `pagination_token` is empty it returns the first page. Non-empty 
`next_pagination_token` and `previous_pagination_token` in the response indicate that there are other pages
available before or after the current page.

Request:

```json
{
  "pagination_token": "bXlsb25ndG9rZW4xCg==",
  "limit": 100
}
```

Response:

```json
{
  "namespaces": [
    {
      "name": "UserObjects",
      "description": "Some description",
      "created_at": 1695826239671432000,
      "updated_at": 1695826239671432000
    }
  ],
  "next_pagination_token": "bXlsb25ndG9rZW4yCg==",
  "previous_pagination_token": "bXlsb25ndG9rZW4xCg=="
}
```

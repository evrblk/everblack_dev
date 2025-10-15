---
title: ListLocks
type: docs
layout: grackle
---

Lists all locks in a given namespace. This is a paginated API. When `pagination_token` is empty it returns the first page.
Non-empty `next_pagination_token` and `previous_pagination_token` in the response indicate that there are other pages
available before or after the current page.

Request:

```json
{
  "namespace_name": "UserObjects",
  "pagination_token": "bXlsb25ndG9rZW4xCg==",
  "limit": 100
}
```

Response:

```json
{
  "locks": [
    {
      "name": "user_object_12345667890",
      "state": "WRITE_LOCKED",
      "locked_at": 1695826239671432000,
      "write_lock_holder": {
        "process_id": "host-123/thread-123456",
        "locked_at": 1695826239671432000,
        "expires_at": 1695826539671432000
      },
      "read_lock_holders": []
    }
  ],
  "next_pagination_token": "bXlsb25ndG9rZW4yCg==",
  "previous_pagination_token": "bXlsb25ndG9rZW4xCg=="
}
```

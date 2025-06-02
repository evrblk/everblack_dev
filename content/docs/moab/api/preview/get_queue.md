---
title: GetQueue
type: docs
layout: moab
---

Returns a queue by name along with all its schedules and current statistics. There is no separate `ListSchedules` method,
instead `GetQueue` should be used to get all schedules for a given queue.

Request:

```json
{
  "queue_name": "SquirrelQueue"
}
```

Response:

```json
{
  "queue": {
    "name": "SquirrelQueue",
    "description": "Async squirrel feeder",
    "created_at": 1695826539671432000,
    "updated_at": 1695826539671432000,
    "version": 1,
    "keepalive_timeout_in_seconds": 15,
    "expires_in_seconds": 1209600,
    "retry_strategy": {
    },
    "dequeuing_settings": {
      "max_inflight_tasks": 0,
      "rate_limiting": {
        "max_tokens": 1000,
        "interval": 1,
        "interval_unit": "SECONDS"
      },
      "dequeuing_paused": false
    },
    "dead_letter_queue_config": {
      "enable": true,
      "max_size": 0,
      "retention_period_in_seconds": 86400
    }
  },
  "schedules": [
    {
      "name": "MySchedule1",
      "description": "Generous feeder",
      "queue_name": "SquirrelQueue",
      "created_at": 1695826549671432000,
      "updated_at": 1695826549671432000,
      "version": 1,
      "cron": "*/5 * * * *",
      "payload": "",
      "dedupe_key": "",
      "expires_in_seconds": 0,
      "keepalive_timeout_in_seconds": 0,
      "retry_strategy": {
      },
      "timezone": "America/Los_Angeles"
    }
  ],
  "stats": {
    "enqueued_tasks_count": 15230, // number of tasks waiting to be picked up
    "inflight_tasks_count": 10, // number of tasks currenly inflight
    "dead_tasks_count": 15, // number of tasks ever died during the lifetime of this queue
    // The oldest task out of this 15230 has been ready to be picked up for 16.5 seconds (in nanoseconds),
    // but it is still in the queue.
    "age_of_oldest_enqueued_task": 16498185433
  }
}
```

__GetQueueRequest__

| Parameter       | Type                |                                                 |
|-----------------|---------------------|-------------------------------------------------|
| queue_name      | String              | Required, max 128 chars, `/[-_0-9a-zA-Z]*/`     |

---
title: Expiration
type: docs
layout: moab
---

A task will expire if it has not been dequeued before its expiration time. Expiration time can be set with optional
parameter `expires_at` when enqueuing (`expires_at` is defined as a timestamp in the future, not a delta). By default,
all tasks will expire in `expires_in_seconds` retention period specified on the queue itself. An expired task will never
be returned from `Dequeue` method.

Internally, all tasks are also indexed by `expires_at` (Expiration index). Pictured below, a task `A` is sheduled at `t1` \
and will expire in `e` seconds (queue retention period) at moment `t1 + e`:

{{< figure src="expiration1.png" class="py-5" >}}

When a task is enqueued it is added to Expiration index on a default or specified expiration time, even if a task
is delayed.

{{< figure src="expiration2.png" class="py-5" >}}

Expiration happens under the hood, tasks will be garbage collected when `expires_at <= now`.

{{< figure src="expiration3.png" class="py-5" >}}

[//]: # (TODO expiration and retries)


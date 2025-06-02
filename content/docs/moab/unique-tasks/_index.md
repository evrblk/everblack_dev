---
title: Unique tasks
type: docs
layout: moab
---

Tasks can be deduplicated by an optional string `dedupe_key`. If a key is set Moab will ensure that at most one task
in `ENQUEUED` or `INFLIGHT` states with such a key can be present in the queue at any given time. Unique (with non-empty
`dedupe_key`) and regular (with empty `dedupe_key`) tasks can be placed into the same queue.

On __Fig. A__ below, task `C` will be successfully enqueued because such a key does not exist yet. On __Fig. B__, task
`C` will be skipped, because such a key exists. Moab does not return errors for duplication, so it will be skipped
silently.

{{< figure src="unique1.png" class="py-5" >}}

However, it is possible to overwrite one or more properties when a duplicate is being enqueued. Moab can overwrite
`payload`, `scheduled_at`, and `expires_at`. Figure below shows how a payload overwrite looks like.

{{< figure src="unique2.png" class="py-5" >}}

Next figure shows how `scheduled_at` can be overwritten. This works for both situations when a task is enqueued at `now`
or into the future. This is handy when something can trigger a delayed job several times, but instead of enqueuing
the same job several times it can be rescheduled instead.

{{< figure src="unique3.png" class="py-5" >}}


__TODO dead?__


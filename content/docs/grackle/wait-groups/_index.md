---
title: Wait Groups
type: docs
layout: grackle
---

Grackle Wait Group tracks the completion of multiple individual jobs. It has similar semantics as `sync.WaitGroup` in 
Go. It is most commonly used for a merge or a fan-in of multiple tasks. It easily supports millions of tasks.

Wait Groups are referenced by name. Names are unique within a namespace. Process IDs are unique within a wait group,
but does not have to be unique between groups.

Wait Groups need to be created upfront with `CreateWaitGroup`. The number of jobs to wait for can be specified at that 
moment. Also, more jobs can be added later with `AddJobToWaitGroup`.

Wait Groups track tasks completion by storing unique `process_id`s for those tasks. If a `process_id` has not been 
reported before, it will be stored and `completed` field on the wait group will be incremented. If a `process_id` has 
been reported before, `completed` field will not be incremented. A wait group is completed when its `completed` equals 
`counter`.
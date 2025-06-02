---
title: Semaphores
type: docs
layout: grackle
---

Grackle Semaphore tracks how many units of a particular resource are available.

Semaphores are referenced by name. Names are unique within a namespace. For example, a name of a resource that you want 
to control can be used as a semaphore name.

Semaphores need to be created upfront with `CreateSemaphore`. The number of permits is specified at that moment.

`AcquireSemaphore` always returns the current semaphore state and `success: true` if a semaphore has been successfully 
held by that request. `AcquireSemaphore` does not throw errors if a semaphore cannot be held (indicated by 
`success: false`) and the current semaphore state can be used to determine what processes hold it.

All holds have a set expiration time (provided with `AcquireSemaphore` request). If a hold is not extended or explicitly
released by that moment, it will become released automatically. There are no hanging semaphores even when a process crashes.

A semaphore can be safely grabbed by the same process multiple times. Repeated `AcquireSemaphore` calls extend semaphore's 
expiration time (if a different `expires_at` is provided) for long-running processes.

`ReleaseSemaphore` releases a hold by a given process. If the process ID from `ReleaseSemaphore` request does not hold 
that semaphore there will be no errors, but nothing will be changed as the result. `DeleteSemaphore` simply deletes a 
semaphore in any state. It can be used to forcefully unlock any semaphore. 

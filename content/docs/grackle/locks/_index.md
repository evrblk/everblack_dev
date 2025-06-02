---
title: Locks
type: docs
layout: grackle
---

Grackle Lock is a **read/write lock**. It can be exclusively locked for writing by a single process, or it can be locked 
for reading by multiple processes. If it is currently locked for writing it cannot be locked for reading, and vise versa.
It can be used it as a mutex if it is locked only for writing by all participating processes.

Locks are referenced by name. Names are unique within a namespace. For example, an ID of a resource that you want to 
control with locking can be used as a lock name.

Locks do not need to be created upfront. Basically, internally Grackle only stores locks that are currently locked. 
`AcquireLock` will grab a lock if it does not currently exist internally. `GetLock` will return an unlocked lock if it
does not currently exist internally.

`AcquireLock` always returns the current lock state and `success: true` if a lock has been successfully locked by that
request. `AcquireLock` does not throw errors if a lock cannot be locked (indicated by `success: false`) and the current
lock state can be used to determine which process holds that lock.

All locks have a set expiration time (provided with `AcquireLock` request). If a lock is not extended or explicitly 
released by that moment, it will become unlocked automatically. There are no hanging locks even when a process crashes.

A lock can be safely grabbed by the same process multiple times. Repeated `AcquireLock` calls extend lock's expiration 
time (if a different `expires_at` is provided) for long-running processes.

`ReleaseLock` unlocks a lock if a given process was holding that lock for writing, or removes that process from the list
of lock holders if it is locked for reading. If the process ID from `ReleaseLock` request does not hold that 
lock there will be no errors, but nothing will be changed as the result. `DeleteLock` simply deletes a lock in any state.
It can be used to forcefully unlock any lock. 

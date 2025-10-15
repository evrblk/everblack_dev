---
title: Concepts
type: docs
layout: grackle
---

Everblack Grackle provides distributed synchronisation primitives: read/write locks, semaphores, and wait groups.

All primitives are organized into **Namespaces**. Primitive names are unique within a namespace.

Primitives are used by **Processes** - parts of a client application. Although this is not enforced by Grackle, 
typically a lock is acquired and released by the same process. For that purpose, processes are referred by 
user-specified IDs. A process ID should refer to the smallest execution thread that makes sense for your application and
language. For example, a combination of a host name and a thread id can uniquely identify each execution thread in 
the cluster of multi-threading applications. In some cases a parent task ID that needs to grab a lock as part of its 
execution can serve as a process ID. In any case each process should be aware of its own ID as it needs to provide it 
every time it acquires or releases a lock.

It is a client's responsibility to acquire a lock before performing an operation that requires locking, and release it 
right after that. It is possible for other processes/applications to check a lock state before performing some operation
if they know a process ID they are interested in.

All Grackle operations are atomic and safe to retry. A client is guaranteed to have grabbed the lock successfully if the
API response says so. Lock re-entry is allowed. Releasing an already released lock does not cause any errors. A job in
a wait group can be reported as completed several times.

Lock and semaphore holds have required expiration time that prevents abandoned holds in case of a process crash. 
Expiration time can be extended for long-running processes while they are holding the lock. 

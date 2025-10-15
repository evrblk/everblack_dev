---
title: Overview
type: docs
layout: grackle
aliases:
  - /docs/grackle/
---

Everblack Grackle provides distributed synchronisation primitives:

* read/write locks
* semaphores
* wait groups (for fan-in or merge)

Grackle state is durable (on disk). All holds have a configurable expiration time. Process crash will not cause a 
dangling lock. Long-running processes can extend the hold. All operations are atomic and safe to retry.

Grackle is Open Source (under AGPL-3 license). It is also available as a fully managed service at Everblack Cloud. The
only difference between OSS and Cloud versions is that there are more advanced APIs to manage API keys and fine-grained
permissions in the cloud.

[Get started with Grackle OSS](/docs/grackle/getting-started).

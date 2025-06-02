---
title: Core Interface
type: docs
layout: monstera
---

A stub can route requests to one or several application cores. Since cores tend to be small, it makes sense to group 
multiple of them in a single stub. An interface for a stub is basically a union of interfaces of corresponding application 
cores. They share the same names and types (protobufs).

To route a request to the right replica Monstera client needs to know:

* **Application name** - a name under which an application core is registered on Monstera nodes.
* **Shard key** - a key for the given unit of work.

There should be enough information in each request to calculate its shard key. There are two ways to do that:

* Pass all necessary information explicitly in the request.
* Encode all necessary information in IDs.

This depends on your use case and ergonomics of the API.

__TODO__

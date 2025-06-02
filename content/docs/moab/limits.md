---
title: Service Limits
type: docs
layout: moab
---

## Soft Limits

Some soft limits are meant to protect other tenants in a multitenant system from a noisy neighbor. Some limits are meant 
to protect the system itself from an abuse. Default limits are opinionated and were designed to fit the majority of normal 
workflows. If any of these soft limits does not fit your particular workflow, please create a request with a desired 
value and a brief description of your use case. You can do this in Account Settings in the Console.

* __Number of queues per account:__ 100
* __Number of schedules per queue:__ 5
* __Total number of schedules per account:__ 50
* __Control Plane API request rate:__
  * __Read methods combined:__ 1k requests per second
  * __Write methods combined:__ 100 requests per second
* __Data Plane API request rate:__
  * __Enqueue per queue:__ 1k requests per second
  * __Dequeue per queue:__ 1k requests per second
  * __All methods combined:__ 5k requests per second
* __Max Dequeue batch size:__ 10 
* __Max Enqueue batch size:__ 10 

Control Plane API read methods:
* GetQueue
* GetSchedule
* ListQueues

Control Plane API write methods:
* CreateQueue
* CreateSchedule
* DeleteQueue
* DeleteSchedule
* UpdateQueue
* UpdateSchedule

Data Plane API methods:
* DeleteTask
* Dequeue
* Enqueue
* GetTask
* PurgeQueue
* RestartTasks

## Hard Limits

Those limits are the result of design tradeoffs and implementation details. However, we might increase them in the future 
as we work on improving the system. 

* __Payload size:__ 64 Kb
* __Name length:__ 128 characters
* __Description length__: 1024 characters
* __Dedupe key length__: 256 characters

---
title: Endpoints
type: docs
layout: api
---

## API

Some services are regional to bring them closer to users. Regions are isolated and resources created in one region are
not visible in another region.

API endpoints for regional services are in the format: `<service>.<region>.api.evrblk.com`.

Regional services:
* `moab`
* `grackle`
* `bison` (coming soon)
* `canyon` (coming soon)

Regions:
* `us-east-2`
* `us-west-1` (coming soon)
* `eu-central-1` (coming soon)

Other services are global, typically for things where latency does not matter much and isolation is not needed. 

Global services:
* `iam`
* `myaccount`

API endpoints for global services are in the format: `<service>.api.evrblk.com`.

Official SDKs build endpoints for you, the only parameter that needs to be specified is the region.

## Console

Console is used to control all services, regional and global. It has a single point of authentication and will provide
a smooth experience when switching between regions.

Regional consoles are available at `<region>.console.evrblk.com`. Global console is available at `console.evrblk.com`.

---
title: Concepts
type: docs
layout: iam
aliases:
  - /docs/iam/
---

Everblack Cloud is an API-first platform. All actions on all services are performed via API calls. The Console also
uses the same public API under the hood. There is no private API or any other workaround. All public APIs have 
fine-grained access controls.

An __Account__ is created when you sign up for the first time. Account holds all resources, manages billing, notification 
and other settings. There are 3 entities for fine-grained access to Everblack services:

* __API keys__
* __Users__
* __Roles__

An __API key__ authenticates all API calls. Read more on [Authentication](/docs/api/authentication). For programmatic
access (such as from SDKs) a pair of an API key ID and a secret should be used as credentials. API keys can be revoked
at any moment.

For Console access __Users__ are used. Users are authenticated by passwords. Under the hood each Console session creates
a temporary API key and holds those credentials in a cookie.

Both users and API key have an associated __Role__ which holds all permissions that those users or keys have. When an 
account is created, a root user is created with the same email. Root user does not have an associated role and can
perform any action on all services and all account operations. Root user cannot be deleted to avoid lockout. All other
users and API keys must have an associated role. Read more on [Authorization](/docs/api/authorization).

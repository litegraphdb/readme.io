---
title: Overview
excerpt: >-
  LiteGraph is a multi-tenant system allowing you to configure separate virtual
  deployments within the same physical deployment.  Each virtual deployment is
  contained within a tenant, and each object within LiteGraph has a tenant
  identifier (GUID) attached to it.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Tenant objects have the following structure:

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Default tenant",
  "Active": true,
  "CreatedUtc": "2025-01-20T02:51:11.325726Z",
  "LastUpdateUtc": "2025-01-20T02:51:11.325727Z"
}
```

## Properties

* **`GUID`** - A globally unique identifier for the tenant, represented as a UUID string.
* **`Name`** - The display name of the tenant.
* **`Active`** - A boolean flag indicating whether the tenant is currently active (`true`) or inactive (`false`).
* **`CreatedUtc`** - The date and time (in UTC) when the tenant was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the tenant object was last updated.
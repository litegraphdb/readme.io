---
title: Overview
excerpt: This section covers api and sdk methods related to tag object.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Structure

tag objects have the following structure:

```json
{
  "GUID": "930212db-ac72-41e7-82f3-323299aade79",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "Key": "mykey",
  "Value": "myvalue",
  "CreatedUtc": "2025-09-04T08:11:15.309359Z",
  "LastUpdateUtc": "2025-09-04T08:11:15.309359Z"
}
```

## Properties

- **`GUID`** - A globally unique identifier for the property, represented as a UUID string.
- **`TenantGUID`** - A globally unique identifier for the tenant associated with the property.
- **`GraphGUID`** - A globally unique identifier for the graph to which the property belongs.
- **`Key`** - The key or name of the property.
- **`Value`** - The value associated with the key.
- **`CreatedUtc`** - The UTC date and time when the property was created.
- **`LastUpdateUtc`** - The UTC date and time when the property was last updated.

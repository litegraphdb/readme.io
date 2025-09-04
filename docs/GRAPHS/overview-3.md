---
title: Overview
excerpt: This section covers api abd sdk methods related to Graph object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Graph objects have the following structure:

```json
{
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Default graph",
  "VectorIndexType": "None",
  "CreatedUtc": "2025-01-20T02:54:27.641013Z",
  "LastUpdateUtc": "2025-01-20T02:54:27.641014Z"
}
```

## Properties

* **`TenantGUID`** - A globally unique identifier for the tenant associated with the graph, represented as a UUID string.
* **`GUID`** - A globally unique identifier for the graph, represented as a UUID string.
* **`Name`** - The name or description of the graph.
* **`VectorIndexType`** - The type of vector index used by the graph (e.g., "None" in this case).
* **`CreatedUtc`** - The date and time (in UTC) when the graph was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the graph object was last updated.
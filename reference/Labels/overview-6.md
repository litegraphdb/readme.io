---
title: Overview
excerpt: This section covers api abd sdk methods related to Label object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Label objects have the following structure:

```json
{
    "GUID": "5a8dd56f-bb32-4ddb-b63f-c1a9cff49652",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Label": "label",
    "CreatedUtc": "2025-09-04T07:54:42.223701Z",
    "LastUpdateUtc": "2025-09-04T07:54:42.223701Z"
}
```

## Properties

* **`GUID`** - A globally unique identifier for the label, represented as a UUID string.
* **`TenantGUID`** - A globally unique identifier for the tenant associated with the label.
* **`GraphGUID`** - A globally unique identifier for the graph to which the label belongs.
* **`Label`** - The name or text of the label.
* **`CreatedUtc`** - The UTC date and time when the label was created.
* **`LastUpdateUtc`** - The UTC date and time when the label was last updated.

---
title: Overview
excerpt: This section covers api and sdk methods related to vector object.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Structure

tag objects have the following structure:

```json
{
  "GUID": "83972a1a-3414-4d3a-8655-474d84e7ce66",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "Model": "all-MiniLM-L6-v2",
  "Dimensionality": 384,
  "Content": "test",
  "Vectors": [0.1, 0.2, 0.3],
  "CreatedUtc": "2025-09-04T08:12:32.893739Z",
  "LastUpdateUtc": "2025-09-04T08:12:32.893739Z"
}
```

## Properties

- **`GUID`** - A globally unique identifier for the vector, represented as a UUID string.
- **`TenantGUID`** - A globally unique identifier for the tenant associated with the vector.
- **`GraphGUID`** - A globally unique identifier for the graph to which the vector belongs.
- **`Model`** - The name of the machine learning model used to generate the vector.
- **`Dimensionality`** - The number of dimensions in the vector.
- **`Content`** - The original content (text, document, etc.) that the vector represents.
- **`Vectors`** - An array of numeric values representing the vector embedding.
- **`CreatedUtc`** - The UTC date and time when the vector was created.
- **`LastUpdateUtc`** - The UTC date and time when the vector was last updated.

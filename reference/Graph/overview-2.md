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
  "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
  "Name": "My graph",
  "VectorIndexType": "None",
  "VectorIndexM": 16,
  "VectorIndexEf": 50,
  "VectorIndexEfConstruction": 200,
  "CreatedUtc": "2025-09-04T08:26:45.592040Z",
  "LastUpdateUtc": "2025-09-04T08:26:45.592040Z",
  "Labels": ["test"],
  "Tags": {
    "Foo": "Bar"
  },
  "Data": {
    "Key": "Value"
  },
  "Vectors": [
    {
      "GUID": "374ec6a9-91d7-412b-9e3f-f1fabac22aab",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "Model": "all-MiniLM-L6-v2",
      "Dimensionality": 384,
      "Content": "test",
      "Vectors": [0.1, 0.2, 0.3],
      "CreatedUtc": "2025-09-04T08:26:45.600435Z",
      "LastUpdateUtc": "2025-09-04T08:26:45.600435Z"
    }
  ]
}
```

## Properties

- **`TenantGUID`** - A globally unique identifier for the tenant associated with the graph, represented as a UUID string.
- **`GUID`** - A globally unique identifier for the graph, represented as a UUID string.
- **`Name`** - The name or description of the graph.
- **`VectorIndexType`** - The type of vector index used by the graph (e.g., "None" in this case).
- **`VectorIndexM`** - The M parameter for the vector index, controlling the number of bi-directional links created for each new element during construction.
- **`VectorIndexEf`** - The ef parameter for the vector index, controlling the size of the dynamic candidate list during search.
- **`VectorIndexEfConstruction`** - The ef_construction parameter for the vector index, controlling the size of the dynamic candidate list during index construction.
- **`CreatedUtc`** - The date and time (in UTC) when the graph was initially created.
- **`LastUpdateUtc`** - The date and time (in UTC) when the graph object was last updated.
- **`Labels`** - An array of string labels associated with the graph.
- **`Tags`** - A key-value object containing custom tags for the graph.
- **`Data`** - A key-value object containing custom data associated with the graph.
- **`Vectors`** - An array of vector objects associated with the graph, each containing:
  - **`GUID`** - A globally unique identifier for the vector, represented as a UUID string.
  - **`TenantGUID`** - A globally unique identifier for the tenant associated with the vector.
  - **`GraphGUID`** - A globally unique identifier for the graph this vector belongs to.
  - **`Model`** - The embedding model used to generate this vector (e.g., "all-MiniLM-L6-v2").
  - **`Dimensionality`** - The number of dimensions in the vector.
  - **`Content`** - The original content that was embedded to create this vector.
  - **`Vectors`** - The actual vector values as an array of floating-point numbers.
  - **`CreatedUtc`** - The date and time (in UTC) when the vector was initially created.
  - **`LastUpdateUtc`** - The date and time (in UTC) when the vector was last updated.

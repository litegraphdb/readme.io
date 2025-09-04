---
title: Overview
excerpt: This section covers api abd sdk methods related to Edge object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Edge objects have the following structure:

```json
{
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "afae4095-1838-40e6-83b7-895601685b92",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "My test edge",
    "From": "f05b8a07-a6c6-4726-bf82-b381cf3cec1b",
    "To": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
    "Cost": 10,
    "CreatedUtc": "2025-08-20T13:28:33.572723Z",
    "LastUpdateUtc": "2025-08-20T13:28:33.572723Z",
    "Labels": [
        "test"
    ],
    "Tags": {
        "test": "true",
        "type": "edge"
    },
    "Data": {
        "Hello": "World"
    },
    "Vectors": [
        {
            "GUID": "a22c8e41-cc90-49ca-8140-54e31a18dcad",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "EdgeGUID": "afae4095-1838-40e6-83b7-895601685b92",
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [
                0.1,
                0.2,
                0.3
            ],
            "CreatedUtc": "2025-08-20T13:28:33.574024Z",
            "LastUpdateUtc": "2025-08-20T13:28:33.574024Z"
        }
    ]
}
```

## Properties

* **`TenantGUID`** - A globally unique identifier for the tenant associated with the edge, represented as a UUID string.
* **`GUID`** - A globally unique identifier for the edge, represented as a UUID string.
* **`GraphGUID`** - A globally unique identifier for the graph associated with the edge, represented as a UUID string.
* **`Name`** - The name or description of the edge.
* **`From`** - The globally unique identifier of the node from which the edge originates.
* **`To`** - The globally unique identifier of the node to which the edge points.
* **`Cost`** - A numerical value representing the cost or weight of the edge.
* **`CreatedUtc`** - The date and time (in UTC) when the edge was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the edge object was last updated.
* **`Labels`** - A list of labels associated with the edge.
* **`Tags`** - A dictionary of key-value pairs representing tags for the edge (e.g., metadata).
* **`Data`** - A dictionary containing additional data related to the edge. Nested structures can be included.
* **`Vectors`** - A list of vectors associated with the edge. Each vector contains its own set of attributes:
  * **`GUID`** - A globally unique identifier for the vector, represented as a UUID string.
  * **`TenantGUID`** - A globally unique identifier for the tenant associated with the vector.
  * **`GraphGUID`** - A globally unique identifier for the graph associated with the vector.
  * **`EdgeGUID`** - A globally unique identifier for the edge associated with the vector.
  * **`Model`** - The machine learning model used for the vector.
  * **`Dimensionality`** - The dimensionality of the vector (i.e., the number of values in the vector).
  * **`Content`** - The content that the vector represents.
  * **`Vectors`** - A list of numeric values representing the vector itself.
  * **`CreatedUtc`** - The date and time (in UTC) when the vector was created.
  * **`LastUpdateUtc`** - The date and time (in UTC) when the vector object was last updated.

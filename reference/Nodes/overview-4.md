---
title: Overview
excerpt: This section covers api abd sdk methods related to Node object.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Structure

Nodeobjects have the following structure:

```json
{
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "My test node",
    "CreatedUtc": "2025-08-20T12:24:34.480419Z",
    "LastUpdateUtc": "2025-08-20T12:24:34.480420Z",
    "Labels": [
        "hello",
        "test"
    ],
    "Tags": {
        "Bar": "Baz",
        "Foo": "Bar"
    },
    "Data": {
        "Hello": "World",
        "Foo": {
            "Data": "hello"
        }
    },
    "Vectors": [
        {
            "GUID": "7af03312-ac01-4e2b-869c-d01041989413",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "NodeGUID": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [
                0.1,
                0.2,
                0.3
            ],
            "CreatedUtc": "2025-08-20T12:24:34.490679Z",
            "LastUpdateUtc": "2025-08-20T12:24:34.490679Z"
        }
    ]
}
```

## Properties

* **`TenantGUID`** - A globally unique identifier for the tenant associated with the node, represented as a UUID string.
* **`GUID`** - A globally unique identifier for the node, represented as a UUID string.
* **`GraphGUID`** - A globally unique identifier for the graph associated with the node, represented as a UUID string.
* **`Name`** - The name or description of the node.
* **`CreatedUtc`** - The date and time (in UTC) when the node was initially created.
* **`LastUpdateUtc`** - The date and time (in UTC) when the node object was last updated.
* **`Labels`** - A list of labels associated with the node.
* **`Tags`** - A dictionary of key-value pairs representing tags for the node (e.g., metadata).
* **`Data`** - A dictionary containing additional data related to the node. Nested structures can be included.
* **`Vectors`** - A list of vectors associated with the node. Each vector contains its own set of attributes:
  * **`GUID`** - A globally unique identifier for the vector, represented as a UUID string.
  * **`TenantGUID`** - A globally unique identifier for the tenant associated with the vector.
  * **`GraphGUID`** - A globally unique identifier for the graph associated with the vector.
  * **`NodeGUID`** - A globally unique identifier for the node associated with the vector.
  * **`Model`** - The machine learning model used for the vector.
  * **`Dimensionality`** - The dimensionality of the vector (i.e., the number of values in the vector).
  * **`Content`** - The content that the vector represents.
  * **`Vectors`** - A list of numeric values representing the vector itself.
  * **`CreatedUtc`** - The date and time (in UTC) when the vector was created.
  * **`LastUpdateUtc`** - The date and time (in UTC) when the vector object was last updated.

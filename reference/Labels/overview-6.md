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

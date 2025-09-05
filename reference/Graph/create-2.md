---
title: Create Graph
excerpt: >-
  Create a new graph in your tenant with optional labels, tags, data, and vector
  embeddings.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Create Graph endpoint allows you to create a new graph within your tenant. A graph serves as a container for nodes, edges, and their associated data, providing the foundation for your knowledge graph structure.

To create a graph, make a `PUT` request to `/v1.0/tenants/{tenant-guid}/graphs` with the graph configuration in the request body.

## Request Parameters

When creating a graph, you can specify the following optional parameters:

* **Name**: A descriptive name for your graph
* **Labels**: An array of string labels to categorize and organize your graph
* **Tags**: Key-value pairs for additional metadata and organization
* **Data**: Custom data object to store application-specific information
* **Vectors**: Array of vector embeddings with model information and dimensionality

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My graph",
    "Labels": [
        "test"
    ],
    "Tags": {
        "Foo": "Bar"
    },
    "Data": {
        "Key": "Value"
    },
    "Vectors": [
        {
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [ 0.1, 0.2, 0.3 ]
        }
    ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createGraph = async () => {
  // Graph object to create
  try {
    const createdGraph = await api.Graph.create({ Name: "New Graph" });
    console.log(createdGraph, "Graph created successfully");
  } catch (err) {
    console.log("err: ", err);
    console.log("Error creating graph:", JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def create_graph():
    graph = litegraph.Graph.create(name="Test Graph",labels=["test"],tags={"Foo": "Bar"},data={"Key": "Value"},vectors=[{"Vectors":[0.1, 0.2, 0.3],"Content":"Test Content","Dimensionality":3,"Model":"all-MiniLM-L6-v2"}])
    print(graph)

create_graph()
```

## Response

```curl
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
    "Labels": [
        "test"
    ],
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
            "Vectors": [
                0.1,
                0.2,
                0.3
            ],
            "CreatedUtc": "2025-09-04T08:26:45.600435Z",
            "LastUpdateUtc": "2025-09-04T08:26:45.600435Z"
        }
    ]
}
```

## Next Steps

After successfully creating a graph, you can:

* Add nodes to populate your graph with entities
* Create edges to establish relationships between nodes
* Perform vector searches for similarity-based queries
* Configure vector indexing for improved search performance

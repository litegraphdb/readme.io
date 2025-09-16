---
title: Get Node Neighbors
excerpt: >-
  Retrieve all neighbor nodes connected to a specific node to analyze its
  immediate connectivity and relationship patterns in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Get Node Neighbors endpoint allows you to discover all neighbor nodes directly connected to a specific node in your graph. This operation is essential for understanding immediate node connectivity, analyzing relationship patterns, and building comprehensive neighbor relationship profiles.

Key capabilities include:

* Finding all neighbor nodes connected to a specific node
* Analyzing immediate connectivity patterns and relationship types
* Discovering all nodes that are directly adjacent to the target node
* Building comprehensive neighbor relationship profiles and connectivity maps
* Supporting immediate graph traversal and neighbor analysis

## Get Node Neighbors

Retrieve all neighbor nodes connected to a specific node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/neighbors`. This endpoint returns all nodes that are directly connected to the specified node, allowing you to analyze the immediate connectivity profile and understand the node's role in the graph structure.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/neighbors' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getNodeNeighbors = async () => {
  try {
    const data = await api.Route.getNodeNeighbors(graphGuid, nodeGuid);
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err), err);
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

def get_neighbors_of_node():
    neighbors = litegraph.RouteNodes.neighbors(
        graph_guid="1cbb2bc5-a990-49a8-9975-e0b1c34d1011",
        node_guid="00000000-0000-0000-0000-000000000000"
    )
    print(neighbors)

get_neighbors_of_node()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<Node> response = liteGraph.Node.ReadNeighbors(Guid.Parse("<tenant-guid>"),
                                                          Guid.Parse("graph-guid"),
                                                          Guid.Parse("node-guid"),
                                                          EnumerationOrderEnum.CreatedDescending);
```

### Response

```json
[
  {
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
    "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My test node",
    "CreatedUtc": "2025-09-09T10:03:05.160383Z",
    "LastUpdateUtc": "2025-09-09T10:03:05.160383Z",
    "Data": {
      "Hello": "World",
      "Foo": {
        "Data": "hello"
      }
    }
  }
]
```

## Best Practices

When retrieving node neighbors, consider the following recommendations:

* **Validate Node GUID**: Ensure the target node GUID exists before making requests
* **Handle Empty Results**: Implement proper handling for nodes with no neighbors

## Next Steps

After retrieving node neighbors, you can:

* Analyze immediate node connectivity patterns and relationship types
* Build comprehensive neighbor relationship profiles and connectivity maps
* Implement immediate graph traversal algorithms for neighbor analysis
* Create node neighbor visualization interfaces
* Perform immediate connectivity analysis and network topology studies
* Develop node-based recommendation systems and neighbor discovery

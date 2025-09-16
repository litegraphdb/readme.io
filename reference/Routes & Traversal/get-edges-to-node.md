---
title: Get Edges To Node
excerpt: >-
  Retrieve all incoming edges to a specific node to analyze its connections and
  incoming relationships in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Get Edges To Node endpoint allows you to discover all incoming connections to a specific node in your graph. This operation is essential for understanding how other nodes connect to a target node, analyzing incoming relationship patterns, and building comprehensive node connectivity profiles.

Key capabilities include:

* Finding all edges that terminate at a specific node
* Analyzing incoming relationship patterns and connection types
* Discovering all nodes that are directly connected to the target node
* Building node connectivity profiles and relationship maps
* Supporting graph traversal and incoming path analysis

## Get Edges To Node

Retrieve all incoming edges to a specific node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges/to`. This endpoint returns all edges that terminate at the specified node, allowing you to analyze the node's incoming connections and understand its role as a destination in the graph structure.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/64058009-3ff7-40e0-b6d8-02252137fb55/edges/to' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getEdgesToNode = async () => {
  try {
    const data = await api.Route.getEdgesToNode(graphGuid, nodeGuid);
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

def get_edges_to_node():
    edges = litegraph.RouteNodes.get_edges_to(graph_guid="graph-guid", node_guid="node-guid")
    print(edges)

get_edges_to_node()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<Edge> response = liteGraph.Edge.ReadEdgesToNode(Guid.Parse("<tenant-guid>"),
                                                            Guid.Parse("<graph-guid>"),
                                                            Guid.Parse("<node-guid>"));
```

### Response

```json
[
  {
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
    "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My test edge",
    "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
    "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
    "Cost": 10,
    "CreatedUtc": "2025-09-09T10:03:46.978477Z",
    "LastUpdateUtc": "2025-09-09T10:03:46.978477Z"
  }
]
```

## Best Practices

When retrieving edges to a node, consider the following recommendations:

* **Validate Node GUID**: Ensure the target node GUID exists before making requests
* **Handle Empty Results**: Implement proper handling for nodes with no incoming edges

## Next Steps

After retrieving edges to a node, you can:

* Analyze the node's incoming relationship patterns and connection types
* Build comprehensive node connectivity profiles and relationship maps
* Implement graph traversal algorithms for incoming path analysis
* Create node relationship visualization interfaces
* Perform incoming connectivity analysis and network topology studies
* Develop node-based recommendation systems and relationship discovery

---
title: Get Edges Between Nodes
excerpt: >-
  Retrieve all edges connecting two specific nodes in your graph for
  relationship analysis and path discovery.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Get Edges Between Nodes endpoint allows you to discover all direct connections between two specific nodes in your graph. This operation is essential for understanding the relationships and pathways that exist between nodes, enabling you to analyze connectivity patterns, identify multiple connection types, and build comprehensive relationship maps.

Key capabilities include:

* Finding all edges that connect two specific nodes
* Analyzing bidirectional relationships between nodes
* Discovering multiple connection types between the same nodes
* Building relationship graphs and connection matrices
* Supporting graph traversal and path-finding algorithms

## Get Edges Between Nodes

Retrieve all edges that directly connect two specific nodes using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/between?from=<from-node-guid>&to=<to-node-guid>`. This endpoint returns all edges that have the specified source and destination nodes, allowing you to analyze the complete relationship structure between any two nodes in your graph.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/between?from=00000000-0000-0000-0000-000000000000&to=00000000-0000-0000-0000-000000000001' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getEdgesBetween = async () => {
  try {
    const data = await api.Route.getEdgesBetween(
      graphGuid,
      fromNodeGuid,
      toNodeGuid
    );
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

def get_edges_between_nodes():
    edges = litegraph.RouteEdges.between(
        graph_guid="graph-guid",
        from_node_guid="node-guid",
        to_node_guid="node-guid-2"
    )
    print(edges)

get_edges_between_nodes()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<Edge> response = liteGraph.Edge.ReadEdgesBetweenNodes(Guid.Parse("<tenant-guid>"),
                                                                  Guid.Parse("<graph-guid>"),
                                                                  Guid.Parse("<from-node-guid>"),
                                                                  Guid.Parse("<to-node-guid>"));
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

When retrieving edges between nodes, consider the following recommendations:

* **Validate Node GUIDs**: Ensure both source and destination node GUIDs exist before making requests
* **Handle Empty Results**: Implement proper handling for cases where no edges exist between nodes
* **Cache Results**: Consider caching edge relationships for frequently accessed node pairs

## Next Steps

After retrieving edges between nodes, you can:

* Analyze the relationship structure and connection patterns
* Build comprehensive node relationship maps
* Implement graph traversal algorithms for path finding
* Create relationship visualization interfaces
* Perform connectivity analysis and network topology studies
* Develop relationship-based recommendation systems

---
title: Get Node Edges
excerpt: Retrieve all edges connected to a specific node to analyze its complete connectivity and relationship patterns in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Get Node Edges endpoint allows you to discover all edges connected to a specific node in your graph, including both incoming and outgoing connections. This operation is essential for understanding complete node connectivity, analyzing relationship patterns, and building comprehensive node relationship profiles.

Key capabilities include:

- Finding all edges connected to a specific node (both incoming and outgoing)
- Analyzing complete node connectivity patterns and relationship types
- Discovering all nodes that are directly connected to the target node
- Building comprehensive node relationship profiles and connectivity maps
- Supporting complete graph traversal and connectivity analysis

## Get Node Edges

Retrieve all edges connected to a specific node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges`. This endpoint returns all edges that are connected to the specified node, including both incoming and outgoing connections, allowing you to analyze the complete connectivity profile of the node.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/edges' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getAllNodeEdges = async () => {
  try {
    const data = await api.Route.getAllNodeEdges(graphGuid, nodeGuid);
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

def get_edges_of_node():
    edges = litegraph.RouteNodes.edges(
        graph_guid="graph-guid",
        node_guid="node-guid"
    )
    print(edges)

get_edges_of_node()
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

When retrieving all node edges, consider the following recommendations:

- **Validate Node GUID**: Ensure the target node GUID exists before making requests
- **Handle Empty Results**: Implement proper handling for nodes with no edges

## Next Steps

After retrieving all node edges, you can:

- Analyze complete node connectivity patterns and relationship types
- Build comprehensive node relationship profiles and connectivity maps
- Implement complete graph traversal algorithms for connectivity analysis
- Create node relationship visualization interfaces
- Perform complete connectivity analysis and network topology studies
- Develop node-based recommendation systems and relationship discovery

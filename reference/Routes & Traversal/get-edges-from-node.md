---
title: Get Edges From Node
excerpt: Retrieve all outgoing edges from a specific node to analyze its connections and outgoing relationships in your graph.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Get Edges From Node endpoint allows you to discover all outgoing connections from a specific node in your graph. This operation is essential for understanding how a node connects to other nodes, analyzing outgoing relationship patterns, and building comprehensive node connectivity profiles.

Key capabilities include:

- Finding all edges that originate from a specific node
- Analyzing outgoing relationship patterns and connection types
- Discovering all nodes that are directly connected from the source node
- Building node connectivity profiles and relationship maps
- Supporting graph traversal and outgoing path analysis

## Get Edges From Node

Retrieve all outgoing edges from a specific node using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges/from`. This endpoint returns all edges that originate from the specified node, allowing you to analyze the node's outgoing connections and understand its role in the graph structure.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/1f56dc61-55d3-48e3-b4a9-d54b864f1763/edges/from' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getEdgesFromNode = async () => {
  try {
    const data = await api.Route.getEdgesFromNode(graphGuid, nodeGuid);
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

def get_edges_from_node():
    edges = litegraph.RouteNodes.get_edges_from(graph_guid="graph-guid", node_guid="node-guid")
    print(edges)

get_edges_from_node()
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

When retrieving edges from a node, consider the following recommendations:

- **Validate Node GUID**: Ensure the source node GUID exists before making requests
- **Handle Empty Results**: Implement proper handling for nodes with no outgoing edges

## Next Steps

After retrieving edges from a node, you can:

- Analyze the node's outgoing relationship patterns and connection types
- Build comprehensive node connectivity profiles and relationship maps
- Implement graph traversal algorithms for outgoing path analysis
- Create node relationship visualization interfaces
- Perform outgoing connectivity analysis and network topology studies
- Develop node-based recommendation systems and relationship discovery

---
title: Sub Graph
excerpt: >-
  Read subgraphs starting from a given node within a graph, and retrieve
  subgraph statistics with configurable traversal depth and node/edge limits.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Sub Graph endpoints provide functionality for extracting and analyzing subgraphs within a larger graph structure. These endpoints allow you to:

- Read a subgraph starting from a specific node with configurable traversal parameters
- Retrieve statistics about a subgraph without fetching the full graph data
- Control traversal depth and limit the number of nodes and edges returned
- Include or exclude node/edge data and subordinate elements

These endpoints are particularly useful for:

- Exploring graph neighborhoods around specific nodes
- Analyzing local graph structures
- Optimizing data retrieval by limiting scope
- Building graph visualization tools
- Implementing graph traversal algorithms

## Read Sub Graph

Read a subgraph starting from a given node within a graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/subgraph`. This endpoint traverses the graph from the specified starting node and returns the subgraph structure based on the provided parameters.

### Query Parameters

The endpoint supports the following optional query parameters:

- **maxDepth**: Maximum traversal depth from the starting node (default: 2). Controls how many levels deep the traversal goes.
- **maxNodes**: Maximum number of nodes to return (default: 0, meaning no limit). Set to 0 for unlimited nodes.
- **maxEdges**: Maximum number of edges to return (default: 0, meaning no limit). Set to 0 for unlimited edges.
- **incldata**: Whether to include node/edge data in the response (default: false). Set to true to include the `Data` property for nodes and edges.
- **inclsub**: Whether to include subordinate/related elements (default: false). Set to true to include subordinate elements in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/subgraph?maxDepth=2&maxNodes=0&maxEdges=0&incldata=false&inclsub=false' \
--header 'Authorization: ••••••'
```

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readSubGraph = async () => {
  try {
    const data = await api.Graph.readSubGraph("<graph-guid>", "<node-guid>", {
      maxDepth: 2,
      maxNodes: 0,
      maxEdges: 0,
      incldata: false,
      inclsub: false,
    });
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
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

def read_subgraph():
    subgraph = litegraph.Graph.read_subgraph(
        graph_guid="graph-guid",
        node_guid="node-guid",
        max_depth=2,
        max_nodes=0,
        max_edges=0,
        incldata=False,
        inclsub=False
    )
    print(subgraph)

read_subgraph()
```

```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
ReadSubGraphResponse response = liteGraph.Graph.ReadSubGraph(
    Guid.Parse("<tenant-guid>"),
    Guid.Parse("<graph-guid>"),
    Guid.Parse("<node-guid>"),
    maxDepth: 2,
    maxNodes: 0,
    maxEdges: 0,
    includeData: false,
    includeSubordinates: false
);
```

### Response

The response contains the subgraph structure with nodes and edges:

```json
{
  "Nodes": [
    {
      "GUID": "00000000-0000-0000-0000-000000000000",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "00000000-0000-0000-0000-000000000000",
      "Name": "Node Name",
      "CreatedUtc": "2025-09-08T10:05:20.543278Z",
      "LastUpdateUtc": "2025-09-08T10:05:20.543278Z"
    }
  ],
  "Edges": [
    {
      "GUID": "00000000-0000-0000-0000-000000000001",
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GraphGUID": "00000000-0000-0000-0000-000000000000",
      "SourceNodeGUID": "00000000-0000-0000-0000-000000000000",
      "TargetNodeGUID": "00000000-0000-0000-0000-000000000002",
      "CreatedUtc": "2025-09-08T10:05:20.543278Z",
      "LastUpdateUtc": "2025-09-08T10:05:20.543278Z"
    }
  ]
}
```

## Read Sub Graph Statistics

Read subgraph statistics for a specific node in a graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/subgraph/stats`. This endpoint provides statistical information about the subgraph without returning the full graph data, making it efficient for analysis and monitoring.

### Query Parameters

The endpoint supports the following optional query parameters:

- **maxDepth**: Maximum traversal depth from the starting node (default: 2). Controls how many levels deep the traversal goes when calculating statistics.
- **maxNodes**: Maximum number of nodes to consider (default: 0, meaning no limit). Set to 0 for unlimited nodes.
- **maxEdges**: Maximum number of edges to consider (default: 0, meaning no limit). Set to 0 for unlimited edges.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/subgraph/stats?maxDepth=2&maxNodes=0&maxEdges=0' \
--header 'Authorization: ••••••'
```

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readSubGraphStatistics = async () => {
  try {
    const data = await api.Graph.readSubGraphStatistics(
      "<graph-guid>",
      "<node-guid>",
      {
        maxDepth: 2,
        maxNodes: 0,
        maxEdges: 0,
      }
    );
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
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

def read_subgraph_statistics():
    statistics = litegraph.Graph.read_subgraph_statistics(
        graph_guid="graph-guid",
        node_guid="node-guid",
        max_depth=2,
        max_nodes=0,
        max_edges=0
    )
    print(statistics)

read_subgraph_statistics()
```

```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
GraphStatistics response = liteGraph.Graph.ReadSubGraphStatistics(
    Guid.Parse("<tenant-guid>"),
    Guid.Parse("<graph-guid>"),
    Guid.Parse("<node-guid>"),
    maxDepth: 2,
    maxNodes: 0,
    maxEdges: 0
);
```

### Response

The response contains statistical information about the subgraph:

```json
{
  "Nodes": 10,
  "Edges": 15,
  "Labels": 3,
  "Tags": 5,
  "Vectors": 2
}
```

## Best Practices

When working with subgraphs, consider the following recommendations:

1. **Traversal Depth**: Use appropriate `maxDepth` values to balance between completeness and performance. Deeper traversals may return large amounts of data.
2. **Node and Edge Limits**: Set `maxNodes` and `maxEdges` to reasonable values to prevent excessive data retrieval, especially for large graphs.
3. **Data Inclusion**: Use `incldata=false` when you only need graph structure, not the full node/edge data, to improve performance.
4. **Statistics First**: Use `readSubGraphStatistics` to get an overview before fetching the full subgraph data.
5. **Error Handling**: Implement proper error handling for cases where the starting node doesn't exist or the graph is empty.
6. **Performance**: For large graphs, consider using statistics endpoints first to estimate the size of the subgraph before retrieval.

## Next Steps

After reading subgraph data, you can:

- Visualize the subgraph structure in graph visualization tools
- Analyze local graph patterns and relationships
- Implement graph traversal and path-finding algorithms
- Build graph exploration interfaces
- Perform network analysis on subgraph structures
- Monitor graph growth and connectivity patterns

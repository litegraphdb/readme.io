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

* Read a subgraph starting from a specific node with configurable traversal parameters
* Retrieve statistics about a subgraph without fetching the full graph data
* Control traversal depth and limit the number of nodes and edges returned
* Include or exclude node/edge data and subordinate elements

These endpoints are particularly useful for:

* Exploring graph neighborhoods around specific nodes
* Analyzing local graph structures
* Optimizing data retrieval by limiting scope
* Building graph visualization tools
* Implementing graph traversal algorithms

## Read Sub Graph

Read a subgraph starting from a given node within a graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/subgraph`. This endpoint traverses the graph from the specified starting node and returns the subgraph structure based on the provided parameters.

### Query Parameters

The endpoint supports the following optional query parameters:

* **maxDepth**: Maximum traversal depth from the starting node (default: 2). Controls how many levels deep the traversal goes.
* **maxNodes**: Maximum number of nodes to return (default: 0, meaning no limit). Set to 0 for unlimited nodes.
* **maxEdges**: Maximum number of edges to return (default: 0, meaning no limit). Set to 0 for unlimited edges.
* **incldata**: Whether to include node/edge data in the response (default: false). Set to true to include the `Data` property for nodes and edges.
* **inclsub**: Whether to include subordinate/related elements (default: false). Set to true to include subordinate elements in the response.

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
    const data = await api.Graph.readSubGraph(
      '00000000-0000-0000-0000-000000000000',
      '2fec5d09-f959-486a-861d-eb9e926eee93',
      {
        maxDepth: 1,
        maxNodes: 0,
        maxEdges: 0,
        incldata: false,
        inclsub: false,
      }
    );
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

readSubGraph()
```

### Response

The response contains the subgraph structure with nodes and edges:

```json
{
    "Graphs": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Default graph",
            "VectorIndexType": "None",
            "VectorIndexM": 16,
            "VectorIndexEf": 50,
            "VectorIndexEfConstruction": 200,
            "CreatedUtc": "2025-08-26T15:38:36.588177Z",
            "LastUpdateUtc": "2025-08-26T15:38:36.588104Z"
        }
    ],
    "Nodes": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "2fec5d09-f959-486a-861d-eb9e926eee93",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Object https://help.juratinc.com/en/collections/8312681-web-app-tutorials:1",
            "CreatedUtc": "2025-11-07T01:59:30.078965Z",
            "LastUpdateUtc": "2025-11-07T01:59:30.078973Z"
        },
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "d3a2a961-0a93-49a0-95f8-da8841b99e57",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Embeddings Document https://help.juratinc.com/en/collections/8312681-web-app-tutorials:1",
            "CreatedUtc": "2025-11-07T01:57:39.417476Z",
            "LastUpdateUtc": "2025-11-07T01:57:39.417487Z"
        },
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "67f796a0-a28b-4b4e-b66b-57e52c014c60",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Source Document https://help.juratinc.com/en/collections/8312681-web-app-tutorials:1",
            "CreatedUtc": "2025-11-07T01:55:59.796671Z",
            "LastUpdateUtc": "2025-11-07T01:55:59.796680Z"
        },
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "5feb0b4a-2b99-4d8c-92c7-775e9f3f6680",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Data Repository Jurat Help",
            "CreatedUtc": "2025-11-05T02:09:13.773020Z",
            "LastUpdateUtc": "2025-11-05T02:09:13.773031Z"
        }
    ],
    "Edges": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "d33aa42e-8023-4d14-a176-34fb26ff6cad",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Object to embeddings document",
            "From": "2fec5d09-f959-486a-861d-eb9e926eee93",
            "To": "d3a2a961-0a93-49a0-95f8-da8841b99e57",
            "Cost": 0,
            "CreatedUtc": "2025-11-07T01:59:38.707060Z",
            "LastUpdateUtc": "2025-11-07T01:59:38.707068Z"
        },
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "bf6f6d12-1e6b-465c-92af-b6c043b648e1",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Object to source document",
            "From": "2fec5d09-f959-486a-861d-eb9e926eee93",
            "To": "67f796a0-a28b-4b4e-b66b-57e52c014c60",
            "Cost": 0,
            "CreatedUtc": "2025-11-07T01:59:38.373899Z",
            "LastUpdateUtc": "2025-11-07T01:59:38.373907Z"
        },
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "c6b52770-9f2b-45bb-a7b8-6221829c6c28",
            "GraphGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Object to data repository",
            "From": "2fec5d09-f959-486a-861d-eb9e926eee93",
            "To": "5feb0b4a-2b99-4d8c-92c7-775e9f3f6680",
            "Cost": 0,
            "CreatedUtc": "2025-11-07T01:59:37.974410Z",
            "LastUpdateUtc": "2025-11-07T01:59:37.974421Z"
        }
    ]
}
```

## Read Sub Graph Statistics

Read subgraph statistics for a specific node in a graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/subgraph/stats`. This endpoint provides statistical information about the subgraph without returning the full graph data, making it efficient for analysis and monitoring.

### Query Parameters

The endpoint supports the following optional query parameters:

* **maxDepth**: Maximum traversal depth from the starting node (default: 2). Controls how many levels deep the traversal goes when calculating statistics.
* **maxNodes**: Maximum number of nodes to consider (default: 0, meaning no limit). Set to 0 for unlimited nodes.
* **maxEdges**: Maximum number of edges to consider (default: 0, meaning no limit). Set to 0 for unlimited edges.

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
      '00000000-0000-0000-0000-000000000000',
      '2fec5d09-f959-486a-861d-eb9e926eee93',
      {
        maxDepth: 1,
        maxNodes: 0,
        maxEdges: 0,
      }
    );
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

readSubGraphStatistics
```

### Response

The response contains statistical information about the subgraph:

```json
{
    "Nodes": 4,
    "Edges": 3,
    "Labels": 4,
    "Tags": 9,
    "Vectors": 0
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

* Visualize the subgraph structure in graph visualization tools
* Analyze local graph patterns and relationships
* Implement graph traversal and path-finding algorithms
* Build graph exploration interfaces
* Perform network analysis on subgraph structures
* Monitor graph growth and connectivity patterns

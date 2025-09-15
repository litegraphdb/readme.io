---
title: Search Nodes
excerpt: >-
  Perform normal and vector-based searches on nodes with advanced filtering,
  expression matching, and semantic similarity capabilities.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Node Search endpoints provide powerful search capabilities for finding nodes within a graph. These endpoints support:

* Normal search with label, tag, and expression-based filtering
* Vector search for semantic similarity and content-based discovery
* Advanced filtering with custom expressions and operators
* Flexible ordering and result pagination
* Integration with graph traversal and relationship analysis

## Normal Search

Perform a standard search on nodes using `POST: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/search`. This endpoint allows you to search nodes based on labels, tags, custom expressions, and ordering preferences.

### Search Parameters

The normal search request supports the following parameters:

* **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
* **Name**: Filter by node name (string, optional)
* **Labels**: Array of labels to filter nodes (array of strings, optional)
* **Tags**: Key-value pairs for tag-based filtering (object, optional)
* **Expr**: Custom expression for advanced filtering (object, optional)

### Expression Parameters

Custom expressions support the following structure:

* **Left**: The field or property to evaluate (string, required)
* **Operator**: The comparison operator (string, required - "Equals", "Contains", "GreaterThan", etc.)
* **Right**: The value to compare against (string/number, required)

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/search' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
  "Ordering": "CreatedDescending",
  "Name": null,
  "Labels": [
    "test"
  ],
  "Tags": {
    "Foo": "Bar"
  },
  "Expr": {
    "Left": "Key",
    "Operator": "Equals",
    "Right": "Value"
  }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";
import { NodeEdgeSearchRequest } from "litegraphdb/dist/types/types";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const searchNodes = async () => {
  const searchRequest: NodeEdgeSearchRequest = {
    GraphGUID: "<graph-guid>",
    Ordering: "CreatedDescending",
    Expr: {
      Left: "Hello",
      Operator: "Equals",
      Right: "World",
    },
  };

  try {
    const response = await api.Node.search(searchRequest);
    console.log(response, "Graph searched successfully");
  } catch (err) {
    console.log("Error searching graph:", JSON.stringify(err), err);
  }
};
```
```
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<VectorSearchResult> response = liteGraph.Vector.SearchNode(VectorSearchTypeEnum.CosineSimilarity,
                                                                       new List<float>() { 0.1f, 0.2f, 0.3f }, 
                                                                       Guid.Parse("tenant-guid"),
                                                                       Guid.Parse("graph-guid"));
```

### Response

```json
{
  "Nodes": [
    {
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "Name": "My test node",
      "CreatedUtc": "2025-09-08T10:18:03.776249Z",
      "LastUpdateUtc": "2025-09-08T10:18:03.776249Z"
    }
  ]
}
```

<br />

## Vector Search

Perform semantic similarity search on nodes using `POST: /v1.0/tenants/{tenant-guid}/vectors`. This endpoint allows you to search for nodes based on vector embeddings and semantic similarity, enabling content-based discovery and similarity matching across your graph data.

### Search Parameters

The vector search request supports the following parameters:

* **GraphGUID**: The graph's unique identifier (string, required)
* **Domain**: The domain to search in (string, required - "Node" for node search)
* **SearchType**: The type of vector search (string, required - "CosineSimilarity", etc.)
* **Labels**: Array of labels to filter nodes (array of strings, optional)
* **Tags**: Key-value pairs for tag-based filtering (object, optional)
* **Expr**: Custom expression for advanced filtering (object, optional)
* **Embeddings**: The vector embeddings to search with (array of numbers, required)

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Domain": "Node",
    "SearchType": "CosineSimilarity",
    "Labels": [],
    "Tags": {},
    "Expr": {},
    "Embeddings": [ 0.1, 0.2, 0.3, 0.5 ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";
import { NodeEdgeSearchRequest } from "litegraphdb/dist/types/types";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const nodeVectorSearch = async () => {
  try {
    const data = await api.Vector.search({
      GraphGUID: "<graph-guid>",
      Domain: "Node",
      SearchType: "Vector",
      Labels: [],
      Tags: {},
      Expr: {},
      Embeddings: [0.1, 0.2, 0.3],
    });
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

```json
[
  {
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
    "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My test node",
    "CreatedUtc": "2025-09-08T10:18:03.776249Z",
    "LastUpdateUtc": "2025-09-08T10:18:03.776249Z"
  }
]
```

<br />

## Next Steps

After successfully searching nodes, you can:

* Process search results and implement result ranking algorithms
* Build advanced search interfaces with filtering and sorting capabilities
* Implement search result caching for improved performance
* Create search analytics and monitoring dashboards
* Develop recommendation systems based on similarity scores
* Build search result visualization and exploration tools
* Implement search result export and sharing functionality
* Set up automated search indexing and optimization processes

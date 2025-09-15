---
title: Vector Search
excerpt: >-
  Perform advanced vector search operations on edges to discover semantically
  similar relationships and implement AI-powered edge discovery.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Vector Search endpoints provide powerful semantic search capabilities for edges in your graph. These operations enable you to discover edges based on semantic similarity, implement AI-powered relationship discovery, and build intelligent edge recommendation systems using vector embeddings and similarity algorithms.

Key capabilities include:

* Performing normal search with filtering and expression-based queries
* Executing vector-based semantic search using embeddings
* Discovering semantically similar edges based on content similarity
* Implementing AI-powered edge discovery and recommendation systems
* Building intelligent relationship mapping and analysis tools

## Normal Search

Perform traditional search operations on edges using filtering, labels, tags, and custom expressions with `POST: v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/search`. This endpoint allows you to search for edges based on specific criteria, enabling precise edge discovery and relationship analysis.

### Search Parameters

The POST request body supports the following parameters:

* **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
* **Name**: Filter edges by name (optional)
* **Labels**: Array of labels to filter edges
* **Tags**: Key-value pairs for tag-based filtering
* **Expr**: Custom expression for advanced filtering with Left, Operator, and Right components

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/search' \
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

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const searchEdges = async () => {
  const searchRequest = {
    GraphGUID: "<graph-guid>",
    Ordering: "CreatedDescending",
    Expr: {
      Left: "Hello",
      Operator: "Equals",
      Right: "World",
    },
  };

  try {
    const response = await api.Edge.search(searchRequest);
    console.log(response, "Edge searched successfully");
  } catch (err) {
    console.log("Error searching edge:", JSON.stringify(err), err);
  }
};
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<VectorSearchResult> response = liteGraph.Vector.SearchEdge(VectorSearchTypeEnum.CosineSimilarity,
                                                                       new List<float>() { 0.1f, 0.2f, 0.3f },
                                                                       Guid.Parse("tenant-guid"),
                                                                       Guid.Parse("graph-guid"));
```

## Vector Search

Perform advanced semantic search on edges using vector embeddings and similarity algorithms with `POST: v1.0/tenants/{tenant-guid}/vectors`. This endpoint enables AI-powered edge discovery by finding semantically similar edges based on their vector representations, allowing you to implement intelligent relationship discovery and recommendation systems.

### Vector Search Parameters

The POST request body supports the following parameters:

* **GraphGUID**: The unique identifier of the graph to search within
* **Domain**: Specify "Edge" to search within edge data
* **SearchType**: Choose similarity algorithm (e.g., "CosineSimilarity")
* **Labels**: Array of labels to filter edges before vector search
* **Tags**: Key-value pairs for tag-based filtering
* **Expr**: Custom expression for additional filtering
* **Embeddings**: Array of numerical values representing the search vector

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Domain": "Edge",
    "SearchType": "CosineSimilarity",
    "Labels": [],
    "Tags": {},
    "Expr": null,
    "Embeddings": [ 0.1, 0.2, 0.3 ]
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

const edgeVectorSearch = async () => {
  try {
    const data = await api.Vector.search({
      GraphGUID: "<graph-guid>",
      Domain: "Edge",
      SearchType: "CosineSimilarity",
      Labels: [],
      Tags: {},
      Expr: null,
      Embeddings: [0.1, 0.2, 0.3],
    });
    console.log(data, "Edge vector search completed");
  } catch (err) {
    console.log("Error in vector search:", JSON.stringify(err));
  }
};
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
IEnumerable<VectorSearchResult> response = liteGraph.Vector.Search(new VectorSearchRequest()
{
    GraphGUID = Guid.Parse("<graph-guid>"),
    Domain = VectorSearchDomainEnum.Node,
    SearchType = VectorSearchTypeEnum.CosineSimilarity,
    Labels = new List<string>(),
    Tags = null,
    Expr = null,
    Embeddings = new List<float>() { 0.1f, 0.2f, 0.3f },
});
```

### Response

```json
[
  {
    "Score": 1,
    "Edge": {
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "Name": "My test edge",
      "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
      "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
      "Cost": 10,
      "CreatedUtc": "2025-09-09T10:03:46.978477Z",
      "LastUpdateUtc": "2025-09-09T10:03:46.978477Z",
      "Data": {
        "Hello": "World"
      },
      "Vectors": [
        {
          "GUID": "8d4d08e6-8bc1-4fe3-9f7f-3a98e38958f0",
          "TenantGUID": "00000000-0000-0000-0000-000000000000",
          "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
          "EdgeGUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
          "Model": "all-MiniLM-L6-v2",
          "Dimensionality": 384,
          "Content": "test",
          "Vectors": [0.1, 0.2, 0.3],
          "CreatedUtc": "2025-09-09T10:03:46.979820Z",
          "LastUpdateUtc": "2025-09-09T10:03:46.979820Z"
        }
      ]
    }
  }
]
```

## Best Practices

When performing vector search on edges, consider the following recommendations:

* **Vector Quality**: Ensure high-quality vector embeddings for accurate similarity results
* **Search Type Selection**: Choose appropriate similarity algorithms (CosineSimilarity, Euclidean, etc.) based on your use case
* **Filtering Strategy**: Use labels and tags to narrow down the search space before vector comparison
* **Performance Optimization**: Consider caching vector search results for frequently accessed queries
* **Result Interpretation**: Analyze similarity scores to understand the relevance of search results

## Next Steps

After performing vector search on edges, you can:

* Implement AI-powered edge recommendation systems based on semantic similarity
* Build intelligent relationship discovery and mapping tools
* Create semantic edge clustering and categorization systems
* Develop content-based edge filtering and organization features
* Implement advanced graph analytics using vector similarity insights
* Build machine learning models for edge relationship prediction

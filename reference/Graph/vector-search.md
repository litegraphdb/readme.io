---
title: Vector Search
excerpt: Perform vector-based similarity searches on graphs and nodes using embeddings, with support for cosine similarity and other vector operations.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Vector Search endpoints enable you to perform similarity-based searches using vector embeddings. These endpoints support two main types of searches:

- **Normal Search**: Traditional graph search with filtering by labels, tags, and expressions
- **Vector Search**: Similarity-based search using vector embeddings for finding semantically similar content

Vector search is particularly useful for:

- Finding similar nodes or graphs based on content
- Implementing recommendation systems
- Performing semantic similarity matching
- Building knowledge discovery applications

## Normal Search

Perform traditional graph search with filtering capabilities using `POST: /v1.0/tenants/{tenant-guid}/graphs/search`. This endpoint allows you to search for graphs based on various criteria including ordering, labels, tags, and custom expressions.

The normal search request supports the following parameters:

- **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
- **Name**: Filter by graph name (optional)
- **Labels**: Array of labels to filter graphs
- **Tags**: Key-value pairs for tag-based filtering
- **Expr**: Custom expression for advanced filtering with Left, Operator, and Right fields

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/search' \
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
import { GraphSearchRequest } from "litegraphdb/dist/types/types";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const searchGraph = async () => {
  const searchRequest: GraphSearchRequest = {
    GraphGUID: "<graph-guid>",
    Ordering: "CreatedDescending",
    Expr: {
      Left: "Hello",
      Operator: "Equals",
      Right: "World",
    },
  };

  try {
    const response = await api.Graph.search(searchRequest);
    console.log(response, "Graph searched successfully");
  } catch (err) {
    console.log("Error searching graph:", JSON.stringify(err), err);
  }
};
```

### Response

```json
{
  "Graphs": [
    {
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "Name": "My graph",
      "VectorIndexType": "None",
      "VectorIndexM": 16,
      "VectorIndexEf": 50,
      "VectorIndexEfConstruction": 200,
      "CreatedUtc": "2025-09-04T08:26:45.592040Z",
      "LastUpdateUtc": "2025-09-04T08:26:45.592040Z"
    }
  ]
}
```

## Vector Search

Perform similarity-based searches using vector embeddings with `POST: /v1.0/tenants/{tenant-guid}/vectors`. This endpoint enables you to find semantically similar content by comparing vector embeddings using various similarity metrics such as cosine similarity.

The vector search request supports the following parameters:

- **GraphGUID**: The unique identifier of the graph to search within
- **Domain**: The domain to search ("Graph" for graphs)
- **SearchType**: The similarity metric to use (e.g: "CosineSimilarity")
- **Labels**: Array of labels to filter results
- **Tags**: Key-value pairs for tag-based filtering
- **Expr**: Custom expression for additional filtering
- **Embeddings**: Array of vector values to use for similarity comparison

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Domain": "Graph",
    "SearchType": "CosineSimilarity",
    "Labels": [],
    "Tags": {},
    "Expr": null,
    "Embeddings": [ 0.1, 0.2, 0.3 ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const graphVectorSearch = async () => {
  try {
    const data = await api.Vector.search({
      GraphGUID: "<graph-guid>",
      Domain: "Graph",
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
    "Score": 1,
    "Graph": {
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GUID": "ee40590e-4f5f-4379-a5b1-68c6ded0dd2c",
      "Name": "My graph",
      "VectorIndexType": "None",
      "VectorIndexM": 16,
      "VectorIndexEf": 50,
      "VectorIndexEfConstruction": 200,
      "CreatedUtc": "2025-09-09T10:20:11.752627Z",
      "LastUpdateUtc": "2025-09-09T10:20:11.752627Z",
      "Data": {
        "Key": "Value"
      },
      "Vectors": [
        {
          "GUID": "2236e461-25fe-4dec-9ea2-c76e49b7f4bd",
          "TenantGUID": "00000000-0000-0000-0000-000000000000",
          "GraphGUID": "ee40590e-4f5f-4379-a5b1-68c6ded0dd2c",
          "Model": "all-MiniLM-L6-v2",
          "Dimensionality": 384,
          "Content": "test",
          "Vectors": [0.1, 0.2, 0.3],
          "CreatedUtc": "2025-09-09T10:20:11.753536Z",
          "LastUpdateUtc": "2025-09-09T10:20:11.753536Z"
        }
      ]
    }
  }
]
```

## Best Practices

When performing vector searches, consider the following recommendations:

1. **Vector Dimensions**: Ensure your embedding vectors match the expected dimensionality
2. **Similarity Metrics**: Choose the appropriate similarity metric for your use case
3. **Filtering**: Combine vector search with label and tag filtering for more precise results
4. **Performance**: Use appropriate pagination for large result sets
5. **Embedding Quality**: Use high-quality embeddings for better similarity results

## Next Steps

After performing vector searches, you can:

- Analyze similarity scores to understand content relationships
- Implement recommendation systems based on search results
- Build knowledge discovery applications
- Create semantic search interfaces
- Develop content clustering and categorization systems

---
title: Create Vector
excerpt: >-
  Comprehensive guide for creating individual vectors and performing bulk vector
  creation operations, including vector embedding management, model
  configuration, and efficient vector storage for advanced similarity search and
  AI-powered applications.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Vector creation operations enable you to store and manage vector embeddings within your graph database. These operations are essential for implementing advanced AI features such as semantic search, similarity matching, recommendation systems, and machine learning applications. Understanding vector creation is crucial for building intelligent applications that can process and analyze high-dimensional data effectively.

Key capabilities include:

- Creating individual vectors with custom embeddings and metadata
- Performing bulk vector creation for efficient batch processing
- Configuring vector models and dimensionality settings
- Associating vectors with nodes or edges in your graph
- Managing vector content and metadata for search optimization

These operations support various use cases such as semantic search, recommendation engines, content similarity analysis, and AI-powered data processing applications.

## Create Single Vector

Create a single vector using `PUT: /v1.0/tenants/{tenant-guid}/vectors`. This endpoint allows you to store a vector embedding with associated metadata, model information, and content for advanced search and analysis capabilities.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [
        0.1,
        0.2,
        0.3
    ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createVector = async () => {
  try {
    const data = await api.Vector.create({
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      EdgeGUID: "<edge-guid>",
      Model: "all-MiniLM-L6-v2",
      Dimensionality: 384,
      Content: "test",
      Vectors: [0.1, 0.2, 0.3],
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

def create_vector():
    vector = litegraph.Vector.create(
        vectors=[0.1, 0.2, 0.3],
        content="Test Content",
        graph_guid="00000000-0000-0000-0000-000000000000",
        dimensionality=3,
        model="all-MiniLM-L6-v2"
    )
    print(vector)

create_vector()
```

### Response

Upon successful vector creation, the API returns a `201 Created` status code with the created vector object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": null,
  "EdgeGUID": null,
  "Model": "all-MiniLM-L6-v2",
  "Dimensionality": 384,
  "Content": "test",
  "Vectors": [0.1, 0.2, 0.3],
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Create Multiple Vectors

Create multiple vectors in a single operation using `PUT: /v1.0/tenants/{tenant-guid}/vectors/bulk`. This bulk operation allows you to efficiently store multiple vector embeddings with different configurations in one API call, which is useful for batch processing and large-scale vector ingestion.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [
      0.1,
      0.2,
      0.3
    ]
  }
]'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createMultipleVectors = async () => {
  try {
    const data = await api.Vector.createBulk([
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Model: "all-MiniLM-L6-v2",
        Dimensionality: 384,
        Content: "test 1",
        Vectors: [0.1, 0.2, 0.3],
      },
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Model: "all-MiniLM-L6-v2",
        Dimensionality: 390,
        Content: "test 2",
        Vectors: [0.5, 0.7, 0.9],
      },
    ]);
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

def create_multiple_vector():
    vectors = litegraph.Vector.create_multiple([
        {
            "graph_guid": "00000000-0000-0000-0000-000000000000",
            "node_guid": None,
            "edge_guid": None,
            "model": "all-MiniLM-L6-v2",
            "dimensionality": 384,
            "content": "Test Content",
            "vectors": [0.1, 0.2, 0.3]
        },
        {
            "graph_guid": "00000000-0000-0000-0000-000000000000",
            "node_guid": None,
            "edge_guid": None,
            "model": "all-MiniLM-L6-v2",
            "dimensionality": 384,
            "content": "Test Content 2",
            "vectors": [0.4, 0.5, 0.6]
        }
    ])
    print(vectors)

create_multiple_vector()
```

### Response

Upon successful bulk vector creation, the API returns a `201 Created` status code with an array of created vector objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [0.1, 0.2, 0.3],
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Best Practices

When creating vectors, consider the following recommendations:

- **Choose Appropriate Models**: Select vector models that match your use case and data type
- **Validate Dimensionality**: Ensure vector dimensions match your model's expected output
- **Optimize Content**: Use meaningful content descriptions for better search results
- **Batch Operations**: Use bulk creation for multiple vectors to improve performance

## Next Steps

After successfully creating vectors, consider these next actions:

- **Configure Vector Indexes**: Set up HNSW indexes for efficient similarity search
- **Perform Vector Search**: Use the created vectors for semantic search operations
- **Update Vectors**: Modify existing vectors as your data evolves
- **Monitor Performance**: Track vector search performance and optimize as needed
- **Integrate with Applications**: Use vectors in your AI-powered applications
- **Backup Vector Data**: Implement backup strategies for critical vector data

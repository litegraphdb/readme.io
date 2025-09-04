---
title: Create Graph
excerpt: Create a new graph in your tenant with nodes, edges, and vector data.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Create Graph endpoint allows you to create a new graph within your tenant. A graph is a collection of interconnected nodes and edges that can represent relationships, hierarchies, or any structured data model. This endpoint supports creating graphs with labels, tags, custom data, and vector embeddings for semantic search capabilities.

## Endpoint

To create a graph, call `PUT: /v1.0/tenants/{tenant-guid}/graphs`

## Request Parameters

| Parameter | Type   | Required | Description                                    |
| --------- | ------ | -------- | ---------------------------------------------- |
| `Name`    | string | Yes      | A descriptive name for the graph               |
| `Labels`  | array  | No       | Array of string labels to categorize the graph |
| `Tags`    | object | No       | Key-value pairs for additional metadata        |
| `Data`    | object | No       | Custom data object to store with the graph     |
| `Vectors` | array  | No       | Array of vector embeddings for semantic search |

### Vector Object Structure

When including vectors, each vector object should contain:

| Parameter        | Type   | Required | Description                                         |
| ---------------- | ------ | -------- | --------------------------------------------------- |
| `Model`          | string | Yes      | The embedding model used (e.g., "all-MiniLM-L6-v2") |
| `Dimensionality` | number | Yes      | The number of dimensions in the vector              |
| `Content`        | string | Yes      | The text content that was embedded                  |
| `Vectors`        | array  | Yes      | The actual vector values as an array of numbers     |

## Examples

### cURL Example

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer your-auth-token' \
--data '{
    "Name": "My Knowledge Graph",
    "Labels": [
        "knowledge-base",
        "documentation"
    ],
    "Tags": {
        "Environment": "Production",
        "Version": "1.0",
        "Owner": "Development Team"
    },
    "Data": {
        "Description": "A comprehensive knowledge graph for our documentation system",
        "CreatedBy": "admin@company.com",
        "LastModified": "2024-01-15T10:30:00Z"
    },
    "Vectors": [
        {
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "This graph contains documentation and knowledge base information",
            "Vectors": [ 0.1, 0.2, 0.3, 0.4, 0.5 ]
        }
    ]
}'
```

### JavaScript SDK Example

```javascript
import { LiteGraphSdk } from "litegraphdb";

// Initialize the SDK with your server URL, tenant GUID, and API key
const api = new LiteGraphSdk(
  "http://localhost:8701/",
  "your-tenant-guid",
  "your-api-key"
);

const createGraph = async () => {
  try {
    // Define the graph configuration
    const graphConfig = {
      Name: "Product Catalog Graph",
      Labels: ["catalog", "products", "inventory"],
      Tags: {
        Category: "E-commerce",
        Environment: "Production",
        Version: "2.1",
      },
      Data: {
        Description:
          "Graph containing product relationships and inventory data",
        CreatedBy: "catalog-manager@company.com",
        Schema: "product-catalog-v2",
      },
      Vectors: [
        {
          Model: "all-MiniLM-L6-v2",
          Dimensionality: 384,
          Content:
            "Product catalog with categories, brands, and inventory relationships",
          Vectors: [0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8],
        },
      ],
    };

    // Create the graph
    const createdGraph = await api.Graph.create(graphConfig);

    console.log("Graph created successfully:", {
      id: createdGraph.Id,
      name: createdGraph.Name,
      labels: createdGraph.Labels,
      createdAt: createdGraph.CreatedAt,
    });

    return createdGraph;
  } catch (error) {
    console.error("Error creating graph:", {
      message: error.message,
      status: error.status,
      details: error.details,
    });
    throw error;
  }
};

// Execute the function
createGraph()
  .then((graph) => console.log("Graph creation completed"))
  .catch((error) => console.error("Failed to create graph:", error));
```

## Response

Upon successful creation, the API returns a `201 Created` status with the created graph object containing:

```curl
{
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My graph",
    "VectorIndexType": "None",
    "VectorIndexM": 16,
    "VectorIndexEf": 50,
    "VectorIndexEfConstruction": 200,
    "CreatedUtc": "2025-09-04T08:26:45.592040Z",
    "LastUpdateUtc": "2025-09-04T08:26:45.592040Z",
    "Labels": [
        "test"
    ],
    "Tags": {
        "Foo": "Bar"
    },
    "Data": {
        "Key": "Value"
    },
    "Vectors": [
        {
            "GUID": "374ec6a9-91d7-412b-9e3f-f1fabac22aab",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [
                0.1,
                0.2,
                0.3
            ],
            "CreatedUtc": "2025-09-04T08:26:45.600435Z",
            "LastUpdateUtc": "2025-09-04T08:26:45.600435Z"
        }
    ]
}
```

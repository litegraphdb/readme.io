---
title: Create Edge
excerpt: Comprehensive guide for creating individual edges and performing bulk edge creation operations, including edge management, relationship establishment, and efficient edge storage for effective graph connectivity and data modeling.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

Edge creation operations enable you to create and manage edges within your graph database. Edges are fundamental components that establish relationships between nodes, enabling complex graph structures and data modeling. Understanding edge creation is crucial for building interconnected graph databases and implementing effective relationship management systems.

Key capabilities include:

- Creating individual edges with custom names and properties
- Performing bulk edge creation for efficient batch processing
- Establishing relationships between nodes with directional connections
- Managing edge metadata, labels, tags, and vector data
- Supporting weighted edges with cost values for graph algorithms

These operations support various use cases such as relationship modeling, network analysis, data connectivity, and implementing complex graph structures for applications.

## Create Single Edge

Create a single edge using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges`. This endpoint allows you to create a new edge connecting two nodes with custom properties, labels, tags, and vector data for comprehensive relationship modeling.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test edge",
    "From": "00000000-0000-0000-0000-000000000000",
    "To": "00000000-0000-0000-0000-000000000001",
    "Cost": 10,
    "Labels": [
        "test"
    ],
    "Tags": {
        "type": "edge",
        "test": "true"
    },
    "Data": {
        "Hello": "World"
    },
    "Vectors": [
        {
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [ 0.1, 0.2, 0.3 ]
        }
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

const createEdge = async () => {
  // Edge object to create
  const edge = {
    GraphGUID: "<graph-guid>",
    Name: "My test edge",
    From: "<from-node-guid>",
    To: "<to-node-guid>",
    Cost: 10,
    Data: {
      Hello: "World",
    },
  };
  try {
    const createdEdge = await api.Edge.create(edge);
    console.log(createdEdge, "Edge created successfully");
  } catch (err) {
    console.log("err: ", err);
    console.log("Error creating edge:", JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    graph_guid="Graph-Guid",
    access_key="******",
)

def create_edge():
    edge = litegraph.Edge.create(
        from_guid="from-node-guid",
        to_guid="to-node-guid",
        name="My test edge",
        cost=10
    )
    print(edge)

create_edge()


```

### Response

Upon successful edge creation, the API returns a `201 Created` status code with the created edge object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "My test edge",
  "From": "00000000-0000-0000-0000-000000000000",
  "To": "00000000-0000-0000-0000-000000000001",
  "Cost": 10,
  "Labels": ["test"],
  "Tags": {
    "type": "edge",
    "test": "true"
  },
  "Data": {
    "Hello": "World"
  },
  "Vectors": [
    {
      "Model": "all-MiniLM-L6-v2",
      "Dimensionality": 384,
      "Content": "test",
      "Vectors": [0.1, 0.2, 0.3]
    }
  ],
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Create Multiple Edges

Create multiple edges in a single operation using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/bulk`. This bulk operation allows you to efficiently create multiple edges with different properties and relationships in one API call, which is useful for batch relationship creation and complex graph modeling.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    {
        "Name": "DigitalOcean to Control Plane",
        "From": "00000000-0000-0000-0000-000000000000",
        "To": "00000000-0000-0000-0000-000000000001",
        "Cost": 100,
        "Labels": [
            "test"
        ],
        "Tags": {
            "type": "edge",
            "test": "true"
        },
        "Data": {
            "hello": "world"
        }
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

const createMultipleEdges = async () => {
  try {
    const data = await api.Edge.createBulk("<graph-guid>", [
      {
        Name: "DigitalOcean to Control Plane",
        From: "<from-node-guid>",
        To: "<to-node-guid>",
        Cost: 100,
        Labels: ["test"],
        Tags: {
          type: "edge",
          test: "true",
        },
        Data: {
          hello: "world",
        },
        GraphGUID: "<graph-guid>",
      },
    ]);
    console.log(data, "Edges created successfully");
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
    graph_guid="Graph-Guid",
    access_key="******",
)

def create_multiple_edge():
    edges = litegraph.Edge.create_multiple([
        {
            "from_guid": "from-node-guid",
            "to_guid": "to-node-guid",
            "name": "DigitalOcean to Control Plane",
            "cost": 100
        },
        {
            "from_guid": "from-node-guid",
            "to_guid": "to-node-guid",
            "name": "DigitalOcean to Control Plane 2",
            "cost": 100
        }
    ])
    print(edges)

create_multiple_edge()
```

### Response

Upon successful bulk edge creation, the API returns a `201 Created` status code with an array of created edge objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "DigitalOcean to Control Plane",
    "From": "00000000-0000-0000-0000-000000000000",
    "To": "00000000-0000-0000-0000-000000000001",
    "Cost": 100,
    "Labels": ["test"],
    "Tags": {
      "type": "edge",
      "test": "true"
    },
    "Data": {
      "hello": "world"
    },
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Best Practices

When creating edges, consider the following recommendations:

- **Validate Node Existence**: Ensure source and target nodes exist before creating edges
- **Use Descriptive Names**: Choose clear, meaningful edge names for better relationship understanding
- **Consistent Naming**: Establish naming conventions for edges across your graph
- **Bulk Operations**: Use bulk creation for multiple edges to improve performance

## Next Steps

After successfully creating edges, consider these next actions:

- **Update Edges**: Modify existing edges using the update operations
- **Delete Edges**: Remove unnecessary edges to maintain data cleanliness
- **Create New Edges**: Add additional edges based on your analysis
- **Integrate Data**: Use created edges in your application logic
- **Monitor Usage**: Track edge usage patterns for optimization opportunities

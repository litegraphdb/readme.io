---
title: Create Node
excerpt: >-
  Create single or multiple nodes in a graph with labels, tags, data, and vector
  embeddings for advanced graph operations and semantic search capabilities.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Create Node endpoint allows you to add new nodes to a graph within a tenant. This functionality is essential for:

* Building graph structures with interconnected data
* Creating nodes with custom labels and tags for categorization
* Storing structured data and metadata within nodes
* Adding vector embeddings for semantic search and similarity operations
* Supporting both single node and bulk node creation operations

**Important**: Node creation requires appropriate permissions within the tenant and must use a valid authentication token. All nodes are validated before being added to the graph.

## Request Parameters

The node creation request accepts the following properties:

#### Node Properties

* **Name**: A descriptive name for the node (string, required)
* **Labels**: Array of labels for categorizing and filtering nodes (array of strings, optional)
* **Tags**: Key-value pairs for additional metadata and categorization (object, optional)
* **Data**: Custom data object containing any structured information (object, optional)
* **Vectors**: Array of vector embeddings for semantic search operations (array, optional)

#### Vector Properties

Each vector in the Vectors array can contain:

* **Model**: The embedding model used to generate the vectors (string, required)
* **Dimensionality**: The number of dimensions in the vector (number, required)
* **Content**: The text content that was vectorized (string, required)
* **Vectors**: The actual vector values as an array of numbers (array of numbers, required)

## Create Single Node

Create a single node in the graph using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`. This endpoint allows you to create a node with custom properties including name, labels, tags, data, and vector embeddings.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test node",
    "Labels": [
        "test",
        "hello"
    ],
    "Tags": {
        "Foo": "Bar",
        "Bar": "Baz"
    },
    "Data": {
        "Hello": "World",
        "Foo": {
            "Data": "hello"
        }
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

const createNode = async () => {
  // Node object to create
  const node = {
    GUID: "<tenant-guid>",
    GraphGUID: "<graph-guid>",
    Name: "Sample Node",
    Data: {
      key1: "value2",
    },
    CreatedUtc: "2024-10-19T14:35:20.351Z",
  };
  try {
    const createdNode = await api.Node.create(node);
    console.log(createdNode, "Node created successfully");
  } catch (err) {
    console.log("err: ", err);
    console.log("Error creating node:", JSON.stringify(err));
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

def create_node():
    node = litegraph.Node.create(name="Sample Node",data={"type": "service"})
    print(node)

create_node()


```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;
using System.Collections.Specialized;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
Node response = liteGraph.Node.Create(new Node
{
    Name = "My test node",
    Labels = new List<string> { "test", "hello" },
    Tags = new NameValueCollection
    {
        { "Foo", "Bar" },
        { "Bar", "Baz" }
    },
    Data = new
    {
        Hello = "World",
        Foo = new { Data = "hello" }
    },
    Vectors = new List<VectorMetadata>
    {
       new VectorMetadata
       {
           Model = "all-MiniLM-L6-v2",
           Dimensionality = 384,
           Content = "test",
           Vectors = new List<float> { 0.1f, 0.2f, 0.3f }
       }
    }
});
```

### &#x20;Response

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "My test node",
  "Labels": ["test", "hello"],
  "Tags": {
    "Foo": "Bar",
    "Bar": "Baz"
  },
  "Data": {
    "Hello": "World",
    "Foo": {
      "Data": "hello"
    }
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

## Create Multiple Nodes

Create multiple nodes in a single operation using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`. This bulk operation allows you to efficiently create multiple nodes with different properties, labels, and data structures in one API call.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    {
        "Name": "Active Directory",
        "Labels": [
            "test"
        ],
        "Tags": {
            "Type": "ActiveDirectory"
        },
        "Data": {
            "Name": "Active Directory"
        }
    },
    {
        "Name": "Website",
        "Labels": [
            "test"
        ],
        "Tags": {
            "Type": "Website"
        },
        "Data": {
            "Name": "Website"
        }
    }
]'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";
import { NodeCreateRequest } from "litegraphdb/dist/types/types";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const crateMultipleNodes = async () => {
  const newMultipleNodes: NodeCreateRequest[] = [
    {
      Name: "Active Directory",
      Labels: ["test"],
      Tags: {
        Type: "ActiveDirectory",
      },
      Data: {
        Name: "Active Directory",
      },
      GraphGUID: "<graph-guid>",
    },
    {
      Name: "Website",
      Labels: ["test"],
      Tags: {
        Type: "Website",
      },
      Data: {
        Name: "Website",
      },
      GraphGUID: "<graph-guid>",
    },
  ];

  try {
    const createdNode = await api.Node.createBulk(guid, newMultipleNodes);
    console.log(createdNode, "Node created successfully");
  } catch (err) {
    console.log("err: ", err);
    console.log("Error creating node:", JSON.stringify(err));
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

def create_multiple_node():
    nodes = litegraph.Node.create_multiple([
        {
            "name": "Active Directory",
            "data": {
                "type": "service"
            }
        },
        {
            "name": "Website",
            "data": {
                "type": "service"
            }
        }
    ])
    print(nodes)

create_multiple_node()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;
using System.Collections.Specialized;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
List<Node> response = liteGraph.Node.CreateMany(
    Guid.Parse("<tenant-guid>"),
    Guid.Parse("<graph-guid>"),
    new List<Node>()
    {
        new Node()
        {
            Name = "My test node",
            Labels = new List<string> { "test", "hello" },
            Tags = new NameValueCollection
            {
                { "Foo", "Bar" },
                { "Bar", "Baz" }
            },
            Data = new
            {
                Hello = "World",
                Foo = new { Data = "hello" }
            },
        }
    });
```

<br />

### Response

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Active Directory",
    "Labels": ["test"],
    "Tags": {
      "Type": "ActiveDirectory"
    },
    "Data": {
      "Name": "Active Directory"
    },
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000002",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Website",
    "Labels": ["test"],
    "Tags": {
      "Type": "Website"
    },
    "Data": {
      "Name": "Website"
    },
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Next Steps

After successfully creating nodes, you can:

* Create edges to connect nodes and build relationships
* Perform graph traversal and path-finding operations
* Implement vector search for semantic similarity queries
* Set up node indexing for improved query performance
* Create graph analytics and reporting features
* Implement node update and deletion operations
* Build graph visualization and exploration interfaces
* Set up automated node validation and monitoring

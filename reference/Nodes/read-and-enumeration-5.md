---
title: Read and Enumerate Nodes
excerpt: >-
  Read individual nodes, retrieve node statistics, and enumerate multiple
  nodes with filtering and search capabilities including data and subordinate information.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Read and Enumeration endpoints provide comprehensive functionality for retrieving node data from your graph. These endpoints allow you to:

- Read individual nodes by their unique identifier
- Retrieve the first node matching specific criteria
- Read multiple nodes by providing their GUIDs
- Enumerate all nodes in a graph
- Search and filter nodes based on labels, tags, and custom expressions
- Implement pagination for large result sets
- Include additional data and subordinate information in responses

## Read Individual Node

Retrieve a specific node by its unique identifier using the `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}` endpoint.

To include additional information in the response, such as custom data fields and subordinate (child) nodes, use the `incldata` and `inclsub` query parameters in your request.

- `incldata=true` will include the `Data` property for each node in the response.
- `inclsub=true` will include subordinate (child) nodes in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getNodeById = async () => {
  try {
    const data = await api.Node.read(grapGuid, nodeGuid);
    console.log(data, "chk data");
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

def retrieve_node():
    node = litegraph.Node.retrieve(guid="node-guid")
    print(node)

retrieve_node()
```

### Response

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

## Read First Node

Retrieve the first node that matches your specified criteria using `GET: /v1.0/tenants/{tenant-id}/graphs/{graph-guid}/nodes/first`. This endpoint is useful when you need to get a single node result based on ordering, labels, tags, or custom expressions. The request body allows you to specify filtering criteria and ordering preferences.

To include additional information in the response, such as custom data fields and subordinate (child) nodes, use the `incldata` and `inclsub` query parameters in your request.

- `incldata=true` will include the `Data` property for each node in the response.
- `inclsub=true` will include subordinate (child) nodes in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/first' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
  "Ordering": "CreatedDescending",
  "Labels": [ ],
  "Tags": { },
  "Expr": { }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readFirstNode = async () => {
  try {
    const data = await api.Node.readFirst(
      "8e72e2b7-86fe-4f94-8483-547c23c8a833",
      {}
    );
    console.log(data, "chk data");
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

def retrieve_first_node():
    node = litegraph.Node.retrieve_first(graph_guid="graph-guid")
    print(node)

retrieve_first_node()
```

## Read Multiple Nodes by GUIDs

Retrieve multiple specific nodes by providing their GUIDs as query parameters using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes?guids=<node1-guid>,<node2-guid>`. This endpoint allows you to fetch several nodes in a single request by specifying comma-separated GUIDs in the URL query string.

To include additional information in the response, such as custom data fields and subordinate (child) nodes, use the `incldata` and `inclsub` query parameters in your request.

- `incldata=true` will include the `Data` property for each node in the response.
- `inclsub=true` will include subordinate (child) nodes in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyNodes = async () => {
  try {
    const data = await api.Node.readMany(grapGuid, [nodeGuid]);
    console.log(data, "chk data");
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

def retrieve_many_node():
    nodes = litegraph.Node.retrieve_many(guids=["node-guid-1","node-guid-2"],graph_guid="graph-guid")
    print(nodes)

retrieve_many_node()
```

## Read All Nodes

Retrieve all nodes within your graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`. This endpoint returns a complete list of all nodes associated with the specified graph.

To include additional information in the response, such as custom data fields and subordinate (child) nodes, use the `incldata` and `inclsub` query parameters in your request.

- `incldata=true` will include the `Data` property for each node in the response.
- `inclsub=true` will include subordinate (child) nodes in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getNodeList = async () => {
  try {
    const data = await api.Node.readAll(grapGuid);
    console.log(data, "chk data");
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
    graph_guid="Graph-Guid",
    access_key="******",
)

def retrieve_all_node():
    nodes = litegraph.Node.retrieve_all()
    print(nodes)

retrieve_all_node()

```

## Enumeration (GET)

The v2.0 enumeration endpoint `GET: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` provides enhanced enumeration capabilities with improved response formatting and additional metadata. This endpoint is designed for efficient enumeration of large node collections with optimized response structures.

To include additional information in the response, such as custom data fields and subordinate (child) nodes.

- `incldata=true` will include the `Data` property for each node in the response.
- `inclsub=true` will include subordinate (child) nodes in the response.
- `max-keys=<number>` will limit the maximum number of nodes returned in the response.
- `skip=<number>` will skip the specified number of nodes in the result set (useful for pagination).
- `continuationToken=<nodeGUID>` will return results starting after the specified node GUID (useful for pagination).

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateNodes = async () => {
  try {
    const data = await api.Node.enumerate(grapGuid);
    console.log(data, "chk data");
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

def enumerate_node():
    nodes = litegraph.Node.enumerate()
    print(nodes)

enumerate_node()
```

## Enumeration and Search (POST)

The advanced enumeration endpoint `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` provides powerful search and filtering capabilities along with enumeration. This endpoint supports complex query parameters including ordering, pagination, label filtering, tag matching, and custom expressions. It's ideal for applications that need to implement sophisticated node discovery and search functionality.

### Search Parameters

The POST request body supports the following parameters:

- **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
- **IncludeData**: Whether to include custom data in the response
- **IncludeSubordinates**: Whether to include subordinate node information
- **MaxResults**: Maximum number of results to return (for pagination)
- **Skip**: Number of results to skip (for pagination)
- **ContinuationToken**: Token for continuing pagination from a previous request
- **Labels**: Array of labels to filter nodes
- **Tags**: Key-value pairs for tag-based filtering
- **Expr**: Custom expression for advanced filtering

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Ordering": "CreatedDescending",
    "IncludeData": true,
    "IncludeSubordinates": true,
    "MaxResults": 5,
    "Skip": 0,
    "ContinuationToken": null,
    "Labels": [ ],
    "Tags": { },
    "Expr": { }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateAndSearchNodes = async () => {
  try {
    const data = await api.Node.enumerateAndSearch(grapGuid, {
      Ordering: "CreatedDescending",
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
    });
    console.log(data, "chk data");
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

def enumerate_with_query_node():
    nodes = litegraph.Node.enumerate_with_query(
        expr=litegraph.ExprModel(
            Left="Name",
            Operator="Equals",
            Right="Test"
        )
    )
    print(nodes)

enumerate_with_query_node()
```

### Response

```json
{
  "Success": true,
  "Timestamp": {
    "Start": "2025-09-08T10:10:08.720761Z",
    "End": "2025-09-08T10:10:08.731802Z",
    "TotalMs": 11.04,
    "Messages": {}
  },
  "MaxResults": 5,
  "EndOfResults": true,
  "TotalRecords": 2,
  "RecordsRemaining": 0,
  "Objects": [
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
}
```

## Best Practices

When reading and enumerating nodes, consider the following recommendations:

1. **Use Query Parameters**: Leverage `incldata` and `inclsub` parameters to control response size and performance
2. **Implement Pagination**: Use `MaxResults`, `Skip`, and `ContinuationToken` for large datasets
3. **Optimize Queries**: Use specific GUIDs when possible instead of reading all nodes
4. **Filter Results**: Use labels, tags, and expressions to narrow down results
5. **Cache Responses**: Implement caching for frequently accessed node data
6. **Handle Large Results**: Use enumeration endpoints for large node collections
7. **Validate Input**: Always validate GUIDs and query parameters before making requests

## Next Steps

After successfully reading and enumerating nodes, you can:

- Create edges to connect nodes and build relationships
- Perform graph traversal and path-finding operations
- Implement vector search for semantic similarity queries
- Update or delete specific nodes based on query results
- Build node analytics and reporting features
- Create node visualization and exploration interfaces
- Set up automated node monitoring and validation
- Implement node-based business logic and workflows

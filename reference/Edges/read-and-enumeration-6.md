---
title: Read and Enumerate Edges
excerpt: >-
  Comprehensive guide for reading individual edges, retrieving edge statistics,
  and enumerating multiple edges with filtering and search capabilities
  including data and subordinate information.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Read and Enumeration endpoints provide comprehensive functionality for retrieving edge data from your graph. These endpoints allow you to:

* Read individual edges by their unique identifier
* Retrieve the first edge matching specific criteria
* Read multiple edges by providing their GUIDs
* Enumerate all edges in a graph
* Search and filter edges based on labels, tags, and custom expressions
* Implement pagination for large result sets
* Include additional data and subordinate information in responses

## Read Individual Edge

Retrieve a specific edge by its unique identifier using the `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}` endpoint.

To include additional information in the response, such as custom data fields and subordinate (child) edges, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each edge in the response.
* `inclsub=true` will include subordinate (child) edges in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getEdgeById = async () => {
  try {
    const data = await api.Edge.read(guid, edgeGuid);
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

def retrieve_edge():
    edge = litegraph.Edge.retrieve(guid="edgeGuid")
    print(edge)

retrieve_edge()
```

### Response

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

## Read First Edge

Retrieve the first edge that matches your specified criteria using `GET: /v1.0/tenants/{tenant-id}/graphs/{graph-guid}/edges/first`. This endpoint is useful when you need to get a single edge result based on ordering, labels, tags, or custom expressions. The request body allows you to specify filtering criteria and ordering preferences.

To include additional information in the response, such as custom data fields and subordinate (child) edges, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each edge in the response.
* `inclsub=true` will include subordinate (child) edges in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/first' \
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

const readFirstEdge = async () => {
  try {
    const data = await api.Edge.readFirst(guid, {});
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

def retrieve_first_edge():
    edge = litegraph.Edge.retrieve_first(ordering="CreatedDescending", graph_guid="Graph-Guid")
    print(edge)

retrieve_first_edge()
```

## Read Multiple Edges by GUIDs

Retrieve multiple specific edges by providing their GUIDs as query parameters using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges?guids=<edge1-guid>,<edge2-guid>`. This endpoint allows you to fetch several edges in a single request by specifying comma-separated GUIDs in the URL query string.

To include additional information in the response, such as custom data fields and subordinate (child) edges, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each edge in the response.
* `inclsub=true` will include subordinate (child) edges in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyEdges = async () => {
  try {
    const data = await api.Edge.readMany(guid, [edgeGuid]);
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

def retrieve_many_edge():
    edges = litegraph.Edge.retrieve_many(graph_guid="Graph-Guid", guids=["edgeGuid", "edgeGuid2"])
    print(edges)

retrieve_many_edge()
```

## Read All Edges

Retrieve all edges within your graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges`. This endpoint returns a complete list of all edges associated with the specified graph.

To include additional information in the response, such as custom data fields and subordinate (child) edges, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each edge in the response.
* `inclsub=true` will include subordinate (child) edges in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getEdgeList = async () => {
  try {
    const data = await api.Edge.readAll(guid);
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

def retrieve_all_edge():
    edges = litegraph.Edge.retrieve_all()
    print(edges)

retrieve_all_edge()
```

## Enumeration (GET)

The v2.0 enumeration endpoint `GET: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges` provides enhanced enumeration capabilities with improved response formatting and additional metadata. This endpoint is designed for efficient enumeration of large edge collections with optimized response structures.

To include additional information in the response, such as custom data fields and subordinate (child) edges.

* `incldata=true` will include the `Data` property for each edge in the response.
* `inclsub=true` will include subordinate (child) edges in the response.
* `max-keys=<number>` will limit the maximum number of edges returned in the response.
* `skip=<number>` will skip the specified number of edges in the result set (useful for pagination).
* `continuationToken=<edgeGUID>` will return results starting after the specified edge GUID (useful for pagination).

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateEdges = async () => {
  try {
    const data = await api.Edge.enumerate(
      "00000000-0000-0000-0000-000000000000"
    );
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

def enumerate_edge():
    edges = litegraph.Edge.enumerate()
    print(edges)

enumerate_edge()
```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-09T10:03:54.787758Z",
        "End": "2025-09-09T10:03:54.805314Z",
        "TotalMs": 17.56,
        "Messages": {}
    },
    "MaxResults": 1000,
    "EndOfResults": true,
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Name": "My test edge",
            "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
            "Cost": 10,
            "CreatedUtc": "2025-09-09T10:03:46.978477Z",
            "LastUpdateUtc": "2025-09-09T10:03:46.978477Z"
        }
    ]
}
```

<br />

## Enumeration and Search (POST)

The advanced enumeration endpoint `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges` provides powerful search and filtering capabilities along with enumeration. This endpoint supports complex query parameters including ordering, pagination, label filtering, tag matching, and custom expressions. It's ideal for applications that need to implement sophisticated edge discovery and search functionality.

### Search Parameters

The POST request body supports the following parameters:

* **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
* **IncludeData**: Whether to include custom data in the response
* **IncludeSubordinates**: Whether to include subordinate edge information
* **MaxResults**: Maximum number of results to return (for pagination)
* **Skip**: Number of results to skip (for pagination)
* **ContinuationToken**: Token for continuing pagination from a previous request
* **Labels**: Array of labels to filter edges
* **Tags**: Key-value pairs for tag-based filtering
* **Expr**: Custom expression for advanced filtering

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Ordering": "CreatedDescending",
    "IncludeData": false,
    "IncludeSubordinates": false,
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

const enumerateAndSearchEdges = async () => {
  try {
    const data = await api.Edge.enumerateAndSearch(guid, {
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

def enumerate_with_query_edge():
    edges = litegraph.Edge.enumerate_with_query(
        expr=litegraph.ExprModel(
            Left="Name",
            Operator="Equals",
            Right="Test"
        )
    )
    print(edges)

enumerate_with_query_edge()
```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-09T10:04:20.372731Z",
        "End": "2025-09-09T10:04:20.388938Z",
        "TotalMs": 16.21,
        "Messages": {}
    },
    "MaxResults": 5,
    "EndOfResults": true,
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Name": "My test edge",
            "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
            "Cost": 10,
            "CreatedUtc": "2025-09-09T10:03:46.978477Z",
            "LastUpdateUtc": "2025-09-09T10:03:46.978477Z"
        }
    ]
}
```

## Best Practices

When reading and enumerating edges, consider the following recommendations:

1. **Use Query Parameters**: Leverage `incldata` and `inclsub` parameters to control response size and performance
2. **Implement Pagination**: Use `MaxResults`, `Skip`, and `ContinuationToken` for large datasets
3. **Optimize Queries**: Use specific GUIDs when possible instead of reading all edges
4. **Filter Results**: Use labels, tags, and expressions to narrow down results
5. **Cache Responses**: Implement caching for frequently accessed edge data
6. **Handle Large Results**: Use enumeration endpoints for large edge collections
7. **Validate Input**: Always validate GUIDs and query parameters before making requests

## Next Steps

After successfully reading and enumerating edges, you can:

* Create nodes to establish graph structure and relationships
* Perform graph traversal and path-finding operations
* Implement vector search for semantic similarity queries
* Update or delete specific edges based on query results
* Build edge analytics and reporting features
* Create edge visualization and exploration interfaces
* Set up automated edge monitoring and validation
* Implement edge-based business logic and workflows

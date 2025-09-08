---
title: Read and Enumerate Graphs
excerpt: >-
  Read individual graphs, retrieve graph statistics, and enumerate multiple
  graphs with filtering and search capabilities.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Read and Enumeration endpoints provide comprehensive functionality for retrieving graph data from your tenant. These endpoints allow you to:

* Read individual graphs by their unique identifier
* Retrieve graph statistics and metadata
* Enumerate multiple graphs with various filtering options
* Search and filter graphs based on labels, tags, and custom expressions
* Implement pagination for large result sets

## Read Individual Graph

Retrieve a specific graph by its unique identifier using the `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}` endpoint.

To include additional information in the response, such as custom data fields and subordinate (child) graphs, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each graph in the response.
* `inclsub=true` will include subordinate (child) graphs in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getGraphById = async () => {
  try {
    const data = await api.Graph.read(guid);
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

def retrieve_graph():
    graph = litegraph.Graph.retrieve(guid="graph-guid")
    print(graph)

retrieve_graph()
```

### Response

```json
{
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My graph",
    "VectorIndexType": "HnswSqlite",
    "VectorIndexFile": "indexes\\graph-00000000-0000-0000-0000-000000000000-hnsw.db",
    "VectorDimensionality": 384,
    "VectorIndexM": 16,
    "VectorIndexEf": 50,
    "VectorIndexEfConstruction": 200,
    "CreatedUtc": "2025-09-04T08:26:45.592040Z",
    "LastUpdateUtc": "2025-09-04T13:25:45.920512Z"
}
```

<br />

### Read Graph Statistics

Retrieve statistical information about a specific graph using `GET: /v1.0/tenants/{tenant-id}/graphs/{graph-guid}/stats`. This endpoint provides metrics such as node count, edge count etc.

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/stats' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readGraphStatistic = async () => {
  try {
    const data = await api.Graph.readStatistic(guid);
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

def retrieve_statistics():
    statistics = litegraph.Graph.retrieve_statistics(graph_guid="graph-guid")
    print(statistics)

retrieve_statistics()
```

### Response

```json
{
    "Nodes": 0,
    "Edges": 0,
    "Labels": 0,
    "Tags": 0,
    "Vectors": 0
}
```

## Read First Graph

Retrieve the first graph that matches your specified criteria using `GET: /v1.0/tenants/{tenant-id}/graphs/first`. This endpoint is useful when you need to get a single graph result based on ordering, labels, tags, or custom expressions. The request body allows you to specify filtering criteria and ordering preferences.

To include additional information in the response, such as custom data fields and subordinate (child) graphs, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each graph in the response.
* `inclsub=true` will include subordinate (child) graphs in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/first' \
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

const readFirstGraph = async () => {
  try {
    const data = await api.Graph.readFirst({});
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```
```python
import litegraph

import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def read_first_graph():
    graph = litegraph.Graph.read_first(ordering="CreatedDescending")
    print(graph)

read_first_graph()
```

## Read Multiple Graphs by GUIDs

Retrieve multiple specific graphs by providing their GUIDs as query parameters using `GET: /v1.0/tenants/{tenant-id}/graphs?guids=<graph1-guid>,<graph2-guid>`. This endpoint allows you to fetch several graphs in a single request by specifying comma-separated GUIDs in the URL query string.

To include additional information in the response, such as custom data fields and subordinate (child) graphs, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each graph in the response.
* `inclsub=true` will include subordinate (child) graphs in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs?guids=00000000-0000-0000-0000-000000000000%2C00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyTenants = async () => {
  try {
    const data = await api.Tenant.readMany([tenantGuid]);
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

def retrieve_multiple_graph():
    graphs = litegraph.Graph.retrieve_many(["graph-guid","graph-guid-2"])
    print(graphs)

retrieve_multiple_graph()
```

## Read All Graphs

Retrieve all graphs within your tenant using `GET: /v1.0/tenants/{tenant-id}/graphs`. This endpoint returns a complete list of all graphs associated with the specified tenant.

To include additional information in the response, such as custom data fields and subordinate (child) graphs, use the `incldata` and `inclsub` query parameters in your request.

* `incldata=true` will include the `Data` property for each graph in the response.
* `inclsub=true` will include subordinate (child) graphs in the response.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getGraphList = async () => {
  try {
    const data = await api.Graph.readAll();
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

def retrieve_all_graph():
    graphs = litegraph.Graph.retrieve_all()
    print(graphs)

retrieve_all_graph()
```

### Read All Graph Statistics

Retrieve statistical information for all graphs in your tenant using `GET: /v1.0/tenants/{tenant-id}/graphs/stats`. This endpoint provides aggregated statistics across all graphs, including total node counts, edge counts etc.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/stats' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllTenantStatistics = async () => {
  try {
    const data = await api.Tenant.readStatistics();
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

def retrieve_statistics_all():
    statistics = litegraph.Graph.retrieve_statistics()
    print(statistics)

retrieve_statistics_all()
```

### Response

```json
{
    "d913a38a-20fc-4009-a0ec-56229f021885": {
        "Nodes": 0,
        "Edges": 0,
        "Labels": 0,
        "Tags": 0,
        "Vectors": 0
    }
}
```

<br />

## Enumeration (GET)

The v2.0 enumeration endpoint `GET: /v2.0/tenants/{tenant-id}/graphs` provides enhanced enumeration capabilities with improved response formatting and additional metadata. This endpoint is designed for efficient enumeration of large graph collections with optimized response structures.

To include additional information in the response, such as custom data fields and subordinate (child) graphs.

* `incldata=true` will include the `Data` property for each graph in the response.
* `inclsub=true` will include subordinate (child) graphs in the response.
* `max-keys=<number>` will limit the maximum number of graphs returned in the response.
* `skip=<number>` will skip the specified number of graphs in the result set (useful for pagination).
* `continuationToken=<graphGUID>` will return results starting after the specified graph GUID (useful for pagination).

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateGraphs = async () => {
  try {
    const data = await api.Graph.enumerate();
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

def enumerate_graph():
    graphs = litegraph.Graph.enumerate()
    print(graphs)

enumerate_graph()
```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T10:09:02.071499Z",
        "End": "2025-09-08T10:09:02.080128Z",
        "TotalMs": 8.63,
        "Messages": {}
    },
    "MaxResults": 1000,
    "EndOfResults": true,
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Name": "My graph",
            "VectorIndexType": "HnswSqlite",
            "VectorIndexFile": "indexes\\graph-00000000-0000-0000-0000-000000000000-hnsw.db",
            "VectorDimensionality": 384,
            "VectorIndexM": 16,
            "VectorIndexEf": 50,
            "VectorIndexEfConstruction": 200,
            "CreatedUtc": "2025-09-04T08:26:45.592040Z",
            "LastUpdateUtc": "2025-09-04T13:25:45.920512Z"
        }
    ]
}
```

## Enumeration and Search (POST)

The advanced enumeration endpoint `POST: /v2.0/tenants/{tenant-id}/graphs` provides powerful search and filtering capabilities along with enumeration. This endpoint supports complex query parameters including ordering, pagination, label filtering, tag matching, and custom expressions. It's ideal for applications that need to implement sophisticated graph discovery and search functionality.

### Search Parameters

The POST request body supports the following parameters:

* **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
* **IncludeData**: Whether to include custom data in the response
* **IncludeSubordinates**: Whether to include subordinate graph information
* **MaxResults**: Maximum number of results to return (for pagination)
* **Skip**: Number of results to skip (for pagination)
* **ContinuationToken**: Token for continuing pagination from a previous request
* **Labels**: Array of labels to filter graphs
* **Tags**: Key-value pairs for tag-based filtering
* **Expr**: Custom expression for advanced filtering

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
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

const enumerateAndSearchGraphs = async () => {
  try {
    const data = await api.Graph.enumerateAndSearch({
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
    access_key="******",
)

def enumerate_with_query_graph():
    graphs = litegraph.Graph.enumerate_with_query(
        ordering="CreatedDescending",
        MaxResults=10,
        Skip=0,
        IncludeData=True,
        IncludeSubordinates=True,
        Expr=litegraph.ExprModel(
            Left="Name",
            Operator="Equals",
            Right="Test"
        )
    )
    print(graphs)

enumerate_with_query_graph()
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
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Name": "My graph",
            "VectorIndexType": "HnswSqlite",
            "VectorIndexFile": "indexes\\graph-00000000-0000-0000-0000-000000000000-hnsw.db",
            "VectorDimensionality": 384,
            "VectorIndexM": 16,
            "VectorIndexEf": 50,
            "VectorIndexEfConstruction": 200,
            "CreatedUtc": "2025-09-04T08:26:45.592040Z",
            "LastUpdateUtc": "2025-09-04T13:25:45.920512Z"
        }
    ]
}
```

<br />

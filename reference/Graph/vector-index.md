---
title: Vector Index Management
excerpt: >-
  Manage vector indexes for graphs including configuration, statistics,
  enabling, rebuilding, and deletion operations for optimized vector search
  performance.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Vector Index Management endpoints allow you to configure and manage vector indexes for your graphs. Vector indexes are essential for efficient similarity-based searches and significantly improve the performance of vector operations. These endpoints provide functionality for:

* Reading vector index configuration and statistics
* Enabling vector indexes with custom parameters
* Rebuilding indexes to optimize performance
* Deleting indexes when no longer needed

Vector indexes are particularly important for:

* Accelerating vector similarity searches
* Supporting large-scale vector operations
* Optimizing memory usage for vector data
* Enabling real-time vector search capabilities

## Read Configuration

Retrieve the current vector index configuration for a graph using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/config`. This endpoint returns the current index settings including type, parameters, and status information.

```curl
curl --location --request GET 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/config' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readVectorIndexConfig = async () => {
  try {
    const data = await api.Graph.readVectorIndexConfig(guid);
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
    access_key="******"
)

def read_config():
    config = litegraph.VectorIndex.get_config(graph_guid="graph-guid")
    print(config)

read_config()
```

### Response

```json
{
  "VectorIndexType": "HnswSqlite",
  "VectorIndexFile": "graph-00000000-0000-0000-0000-000000000000-hnsw.db",
  "VectorDimensionality": 384,
  "VectorIndexM": 16,
  "VectorIndexEf": 50,
  "VectorIndexEfConstruction": 200
}
```

## Read Statistics

Retrieve performance statistics and metrics for the vector index using `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/stats`. This endpoint provides insights into index performance, size, and usage metrics.

```curl
curl --location --request GET 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/stats' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readVectorIndexStats = async () => {
  try {
    const data = await api.Graph.readVectorIndexStats(guid);
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

def get_stats():
    stats = litegraph.VectorIndex.get_stats(graph_guid="graph-guid")
    print(stats)

get_stats()
```

### Response

```json
{
  "VectorCount": 0,
  "Dimensions": 384,
  "IndexType": "HnswSqlite",
  "M": 16,
  "EfConstruction": 200,
  "DefaultEf": 50,
  "IndexFile": "indexes\\graph-00000000-0000-0000-0000-000000000000-hnsw.db",
  "IndexFileSizeBytes": 0,
  "EstimatedMemoryBytes": 0,
  "LastRebuildUtc": "2025-09-04T13:25:45.912460Z",
  "IsLoaded": true,
  "DistanceMetric": "Cosine"
}
```

## Enable Vector Index

Enable a vector index for a graph using `PUT: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/enable`. This endpoint allows you to configure and activate vector indexing with custom parameters to optimize search performance.

### Configuration Parameters

The enable request supports the following parameters:

* **VectorIndexType**: The type of vector index to use (e.g., "HnswSqlite")
* **VectorIndexFile**: The filename for the index storage
* **VectorIndexThreshold**: Optional threshold value for index operations
* **VectorDimensionality**: The dimensionality of vectors in the index
* **VectorIndexM**: The number of bi-directional links for each node (HNSW parameter)
* **VectorIndexEf**: The size of the dynamic candidate list (HNSW parameter)
* **VectorIndexEfConstruction**: The size of the dynamic candidate list during construction (HNSW parameter)

```curl
curl --location --request PUT 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/enable' \
--header 'Authorization: Bearer litegraphadmin' \
--header 'Content-Type: application/json' \
--data-raw '{
    "VectorIndexType": "HnswSqlite",
    "VectorIndexFile": "graph-00000000-0000-0000-0000-000000000000-hnsw.db",
    "VectorIndexThreshold": null,
    "VectorDimensionality": 384,
    "VectorIndexM": 16,
    "VectorIndexEf": 50,
    "VectorIndexEfConstruction": 200
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enableVectorIndex = async () => {
  try {
    const data = await api.Graph.enableVectorIndex(guid, {
      VectorIndexType: "HnswSqlite",
      VectorIndexFile: "graph-00000000-0000-0000-0000-000000000000-hnsw.db",
      VectorIndexThreshold: null,
      VectorDimensionality: 384,
      VectorIndexM: 16,
      VectorIndexEf: 50,
      VectorIndexEfConstruction: 200,
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

def enable_vector_index():
    vector_index = litegraph.VectorIndex.enable(
        graph_guid="00000000-0000-0000-0000-000000000000", 
        config=litegraph.HnswLiteVectorIndexModel(
            VectorIndexType="HnswSqlite", 
            VectorIndexFile="graph-00000000-0000-0000-0000-000000000000-hnsw.db", 
            VectorDimensionality=384, 
            M=16, 
            DefaultEf=50, 
            EfConstruction=200
        )
    )
    print(vector_index)

enable_vector_index()
```

### Response

```json
{
  "VectorIndexType": "HnswSqlite",
  "VectorIndexFile": "graph-00000000-0000-0000-0000-000000000000-hnsw.db",
  "VectorDimensionality": 384,
  "VectorIndexM": 16,
  "VectorIndexEf": 50,
  "VectorIndexEfConstruction": 200
}
```

## Rebuild Vector Index

Rebuild the vector index to optimize performance and update the index structure using `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/rebuild`. This operation is useful when the index becomes fragmented or when you want to optimize performance after significant data changes.

```curl
curl --location --request POST 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/rebuild' \
--header 'Authorization: Bearer litegraphadmin' \
--data-raw ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const rebuildVectorIndex = async () => {
  try {
    const data = await api.Graph.rebuildVectorIndex(guid);
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

def rebuild_vector_index():
    vector_index = litegraph.VectorIndex.rebuild(
        graph_guid="graph-guid", 

    )
    print(vector_index)

rebuild_vector_index()
```

### Response

Upon successful rebuild, the API returns a `200 OK` status code. No response body is returned for this operation.

## Delete Vector Index

Remove the vector index for a graph using `DELETE: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex`. This operation permanently removes the index and all associated data. Use this when you no longer need vector search capabilities for the graph.

```curl
curl --location --request DELETE 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex' \
--header 'Authorization: Bearer litegraphadmin' \
--data-raw ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteVectorIndex = async () => {
  try {
    const data = await api.Graph.deleteVectorIndex(guid);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

Upon successful delete, the API returns a `200 OK` status code. No response body is returned for this operation.

## Next Steps

After managing vector indexes, you can:

* Perform optimized vector similarity searches
* Monitor index performance and statistics
* Implement vector-based recommendation systems
* Build semantic search applications
* Optimize vector operations for large-scale deployments

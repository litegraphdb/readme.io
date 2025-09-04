---
title: Vector Index
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read Configuration

read the configuration of the vectorIndex call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/config`

```curl
curl --location --request GET 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/config' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readVectorIndexConfig = async () => {
  try {
    const data = await api.Graph.readVectorIndexConfig(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read Statistics

read the statistics of the configuration call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/stats`

```curl
curl --location --request GET 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/stats' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readVectorIndexStats = async () => {
  try {
    const data = await api.Graph.readVectorIndexStats(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Enable Vector Index

to enable vectorIndex call `PUT: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/enable`

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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enableVectorIndex = async () => {
  try {
    const data = await api.Graph.enableVectorIndex(guid, {
      VectorIndexType: 'HnswSqlite',
      VectorIndexFile: 'graph-00000000-0000-0000-0000-000000000000-hnsw.db',
      VectorIndexThreshold: null,
      VectorDimensionality: 384,
      VectorIndexM: 16,
      VectorIndexEf: 50,
      VectorIndexEfConstruction: 200,
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Rebuild Vector Index

to rebuild vectoe index call `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex/rebuild`

```curl
curl --location --request POST 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/rebuild' \
--header 'Authorization: Bearer litegraphadmin' \
--data-raw ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const rebuildVectorIndex = async () => {
  try {
    const data = await api.Graph.rebuildVectorIndex(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete Vector Index

to delete vector index call `DELETE: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/vectorindex`

```curl
curl --location --request DELETE 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex' \
--header 'Authorization: Bearer litegraphadmin' \
--data-raw ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteVectorIndex = async () => {
  try {
    const data = await api.Graph.deleteVectorIndex(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

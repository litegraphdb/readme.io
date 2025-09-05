---
title: Read and Enumeration
excerpt: Read and Enumerate nodes.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

Read a single node: `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');


const getNodeById = async () => {
  try {
    const data = await api.Node.read(grapGuid, nodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
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

def retrieve_node():
    node = litegraph.Node.retrieve(guid="node-guid")
    print(node)

retrieve_node()
```

## Read first

Read a first node: `/v1.0/tenants/{tenant-id}/graphs/{graph-guid}/nodes/first`

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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readFirstNode = async () => {
  try {
    const data = await api.Node.readFirst('8e72e2b7-86fe-4f94-8483-547c23c8a833', {});
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

## Read by GUIDs

To Read multiple nodes call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes?guids=<node1-guid>,<node2-guid>`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readManyNodes = async () => {
  try {
    const data = await api.Node.readMany(grapGuid, [nodeGuid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Read all

To read all nodes call `GET:/v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getNodeList = async () => {
  try {
    const data = await api.Node.readAll(grapGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};

```

## Enumeration (GET)

Enumeration via `GET:/v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` allows to enumerate response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateNodes = async () => {
  try {
    const data = await api.Node.enumerate(grapGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Enumeration and search (POST)

Enumeration via `POST :/v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` allows to enumerate and search response

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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateAndSearchNodes = async () => {
  try {
    const data = await api.Node.enumerateAndSearch(grapGuid, {
      Ordering: 'CreatedDescending',
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};


```

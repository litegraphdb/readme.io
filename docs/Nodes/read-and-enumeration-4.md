---
title: Read and Enumeration
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
    const data = await api.Node.read(guid, nodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read by GUIDs

To Read multiple credentials call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes?guids=<node1-guid>,<node2-guid>`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readManyNodes = async () => {
  try {
    const data = await api.Node.readMany(guid, [nodeGuid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Read all

To read all credentials call `GET:/v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readAllCredentials = async () => {
  try {
    const data = await api.Credential.readAll();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Enumeration (GET)

Enumeration via `GET:/v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` allows to enumerate response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateCredentials = async () => {
  try {
    const data = await api.Credential.enumerate();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};


```

## Enumeration and search (POST)

Enumeration via `POST :/v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes` allows to enumerate and search response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateAndSearchCredentials = async () => {
  try {
    const data = await api.Credential.enumerateAndSearch({
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
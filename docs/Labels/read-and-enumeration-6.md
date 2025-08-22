---
title: Read and Enumeration
excerpt: Read and Enumerate labels.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

Read a single label: `GET: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');


const getEdgeById = async () => {
  try {
    const data = await api.Edge.read(guid, edgeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Read by GUIDs

To Read multiple labels call `GET: /v1.0/tenants/{tenant-guid}/labels?guids=<label1-guid>,<label2-guid>`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readManyLabels = async () => {
  try {
    const data = await api.Label.readMany([labelGuid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Read all

To read all labels call `GET:/v1.0/tenants/{tenant-guid}/labels`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readAllLabels = async () => {
  try {
    const data = await api.Label.readAll();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Enumeration (GET)

Enumeration via `GET:/v2.0/tenants/{tenant-guid}/labels` allows to enumerate response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const enumerateLabels = async () => {
  try {
    const data = await api.Label.enumerate();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Enumeration and search (POST)

Enumeration via `POST :/v2.0/tenants/{tenant-guid}/labels` allows to enumerate and search response

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/labels' \
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

const enumerateAndSearchLabels = async () => {
  try {
    const data = await api.Label.enumerateAndSearch({
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
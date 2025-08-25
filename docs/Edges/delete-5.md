---
title: Delete
excerpt: Delete existing edge.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single edge

To delete existing edge call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteEdgeById = async () => {
  try {
    const data = await api.Edge.delete(guid, edgeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete multiple edge

To delete multiple edges call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/bulk`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteMultipleEdges = async () => {
  try {
    const data = await api.Edge.deleteBulk(guid, [edge-guid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete all edges

To delete existing edge call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/all`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/all' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteAllEdges = async () => {
  try {
    const data = await api.Node.deleteAll(<graph-guid>);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

---
title: Create
excerpt: Create Tag.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Create single tag

To create single tag call `PUT: /v1.0/tenants/{tenant-guid}/tags`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue"
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createTag = async () => {
  try {
    const data = await api.Tag.create({
      GraphGUID: '<graph-guid>',
      NodeGUID: '<node-guid>',
      EdgeGUID: '<edge-guid>',
      Key: 'mykey',
      Value: 'myvalue',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Create multiple label

To create multiple tag call `PUT: /v1.0/tenants/{tenant-guid}/tags/bulk`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue"
  }
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createMultipleTags = async () => {
  try {
    const data = await api.Tag.createBulk([
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Key: 'mykey test',
        Value: 'myvalue test',
      },
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Key: 'mykey test 2',
        Value: 'myvalue test 2',
      },
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

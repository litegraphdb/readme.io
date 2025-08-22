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
      GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
      NodeGUID: 'b8837eb9-b180-479f-b09e-d3ad8adab9ee',
      EdgeGUID: 'e9702f09-cd73-413b-8e00-5f871472a02d',
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
        GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
        NodeGUID: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
        EdgeGUID: '53b94bd9-98ea-47e6-9e5a-4fe346298717',
        Key: 'mykey test',
        Value: 'myvalue test',
      },
      {
        GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
        NodeGUID: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
        EdgeGUID: '53b94bd9-98ea-47e6-9e5a-4fe346298717',
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
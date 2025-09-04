---
title: Create
excerpt: Create Vector.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Create single vector

To create single vector call `PUT: /v1.0/tenants/{tenant-guid}/vectors`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [
        0.1,
        0.2,
        0.3
    ]
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createVector = async () => {
  try {
    const data = await api.Vector.create({
      GraphGUID: '<graph-guid>',
      NodeGUID: '<node-guid>',
      EdgeGUID: '<edge-guid>',
      Model: 'all-MiniLM-L6-v2',
      Dimensionality: 384,
      Content: 'test',
      Vectors: [0.1, 0.2, 0.3],
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Create multiple Vector

To create multiple vector call `PUT: /v1.0/tenants/{tenant-guid}/vectors/bulk`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Model": "all-MiniLM-L6-v2",
    "Dimensionality": 384,
    "Content": "test",
    "Vectors": [
      0.1,
      0.2,
      0.3
    ]
  }
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createMultipleVectors = async () => {
  try {
    const data = await api.Vector.createBulk([
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Model: 'all-MiniLM-L6-v2',
        Dimensionality: 384,
        Content: 'test 1',
        Vectors: [0.1, 0.2, 0.3],
      },
      {
        GraphGUID: '<graph-guid>',
        NodeGUID: '<node-guid>',
        EdgeGUID: '<edge-guid>',
        Model: 'all-MiniLM-L6-v2',
        Dimensionality: 390,
        Content: 'test 2',
        Vectors: [0.5, 0.7, 0.9],
      },
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

---
title: Create
excerpt: Create edge.
deprecated: false
hidden: false
metadata:
  robots: index
---
Include bulk creation

## Create single edge

To create single node call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test edge",
    "From": "00000000-0000-0000-0000-000000000000",
    "To": "00000000-0000-0000-0000-000000000001",
    "Cost": 10,
    "Labels": [
        "test"
    ],
    "Tags": {
        "type": "edge",
        "test": "true"
    },
    "Data": {
        "Hello": "World"
    },
    "Vectors": [
        {
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [ 0.1, 0.2, 0.3 ]
        }
    ]
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createEdge = async () => {
  // Edge object to create
  const edge = {
    GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
    Name: 'My test edge',
    From: '2b1520be-d285-4f22-8c74-f296047162b9',
    To: '784cfa37-fb06-4f81-b10d-f1167dfe2b22',
    Cost: 10,
    Data: {
      Hello: 'World',
    },
  };
  try {
    const createdEdge = await api.Edge.create(edge);
    console.log(createdEdge, 'Edge created successfully');
  } catch (err) {
    console.log('err: ', err);
    console.log('Error creating edge:', JSON.stringify(err));
  }
};

```

## Create multiple edge

To create multiple node call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/bulk`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    {
        "Name": "DigitalOcean to Control Plane",
        "From": "00000000-0000-0000-0000-000000000000",
        "To": "00000000-0000-0000-0000-000000000001",
        "Cost": 100,
        "Labels": [
            "test"
        ],
        "Tags": {
            "type": "edge",
            "test": "true"
        },
        "Data": {
            "hello": "world"
        }
    }
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createMultipleEdges = async () => {
  try {
    const data = await api.Edge.createBulk('00900db5-c9b7-4631-b250-c9e635a9036e', [
      {
        Name: 'DigitalOcean to Control Plane',
        From: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
        To: '38eff321-7eaa-457e-b5e0-5f7fa7041e63',
        Cost: 100,
        Labels: ['test'],
        Tags: {
          type: 'edge',
          test: 'true',
        },
        Data: {
          hello: 'world',
        },
        GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
      },
    ]);
    console.log(createdNode, 'Node created successfully');;
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```
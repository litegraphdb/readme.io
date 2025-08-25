---
title: Create
excerpt: Create edge.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Create single edge

To create single edge call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges`

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
    GraphGUID: '<graph-guid>',
    Name: 'My test edge',
    From: '<from-node-guid>',
    To: '<to-node-guid>',
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

To create multiple edge call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/bulk`

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
    const data = await api.Edge.createBulk('<graph-guid>', [
      {
        Name: 'DigitalOcean to Control Plane',
        From: '<from-node-guid>',
        To: '<to-node-guid>',
        Cost: 100,
        Labels: ['test'],
        Tags: {
          type: 'edge',
          test: 'true',
        },
        Data: {
          hello: 'world',
        },
        GraphGUID: '<graph-guid>',
      },
    ]);
    console.log(createdNode, 'Node created successfully');;
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

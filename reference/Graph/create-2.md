---
title: Create
excerpt: Create graph.
deprecated: false
hidden: false
metadata:
  robots: index
---
To create graph call `PUT: /v1.0/tenants/{tenant-guid}/graphs`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My graph",
    "Labels": [
        "test"
    ],
    "Tags": {
        "Foo": "Bar"
    },
    "Data": {
        "Key": "Value"
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

const createGraph = async () => {
  // Graph object to create
  try {
    const createdGraph = await api.Graph.create({ Name: 'New Graph' });
    console.log(createdGraph, 'Graph created successfully');
  } catch (err) {
    console.log('err: ', err);
    console.log('Error creating graph:', JSON.stringify(err));
  }
};
```

## Response

Upon successful creation, the API returns a `201 Created` status with the created graph object containing:

```curl
{
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GUID": "d913a38a-20fc-4009-a0ec-56229f021885",
    "Name": "My graph",
    "VectorIndexType": "None",
    "VectorIndexM": 16,
    "VectorIndexEf": 50,
    "VectorIndexEfConstruction": 200,
    "CreatedUtc": "2025-09-04T08:26:45.592040Z",
    "LastUpdateUtc": "2025-09-04T08:26:45.592040Z",
    "Labels": [
        "test"
    ],
    "Tags": {
        "Foo": "Bar"
    },
    "Data": {
        "Key": "Value"
    },
    "Vectors": [
        {
            "GUID": "374ec6a9-91d7-412b-9e3f-f1fabac22aab",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "Model": "all-MiniLM-L6-v2",
            "Dimensionality": 384,
            "Content": "test",
            "Vectors": [
                0.1,
                0.2,
                0.3
            ],
            "CreatedUtc": "2025-09-04T08:26:45.600435Z",
            "LastUpdateUtc": "2025-09-04T08:26:45.600435Z"
        }
    ]
}
```

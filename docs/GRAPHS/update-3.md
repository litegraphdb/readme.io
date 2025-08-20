---
title: Update
excerpt: Update existing graph.
deprecated: false
hidden: false
metadata:
  robots: index
---
to update graph call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "Default graph",
    "CreatedUtc": "2025-01-23T19:36:55.209306Z",
    "LastUpdateUtc": "2025-01-23T19:36:55.209219Z",
    "Labels": [
        "graph"
    ],
    "Tags": {
        "type": "graph"
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

const updateGraph = async () => {
  // Graph object to update
  const graph: Graph = {
    TenantGUID: '00000000-0000-0000-0000-000000000000',
    GUID: '08944937-e506-416a-b96e-d7b40344c618',
    LastUpdateUtc: '2024-10-19T14:35:20.351Z',
    Name: 'Sample Node',
    CreatedUtc: '2024-10-19T14:35:20.351Z',
    Data: {
      key1: 'value2',
    },
    Labels: ['test'],
    Tags: {
      Type: 'ActiveDirectory',
    },
    Vectors: [],
  };

  try {
    const updatedGraph = await api.Graph.update(graph);
    console.log(updatedGraph, 'Graph updated successfully');
  } catch (err) {
    console.log('Error creating graph:', JSON.stringify(err));
  }
};
```
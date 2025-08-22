---
title: Update
excerpt: Update existing vectors.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing vector call `PUT: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
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

const updateVector = async () => {
  try {
    const data = await api.Vector.update({
      GUID: '70cd93dd-0f38-435d-b57d-f5d1bc1b4481',
      GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
      NodeGUID: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
      EdgeGUID: '53b94bd9-98ea-47e6-9e5a-4fe346298717',
      Model: 'all-MiniLM-L6-v2',
      Dimensionality: 388,
      Content: 'test',
      Vectors: [0.5, 0.7, 0.9],
      TenantGUID: '',
      CreatedUtc: '',
      LastUpdateUtc: '',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};


```
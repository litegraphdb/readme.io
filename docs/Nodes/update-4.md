---
title: Update
excerpt: Update existing node.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing node call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "My test node 2",
    "Labels": [
        "test",
        "updated"
    ],
    "Tags": {
        "updated": "true"
    },
    "Data": {
        "Updated": "Data"
    }
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateNode = async () => {
  // Node object to update
  const node: Node = {
    TenantGUID: '00000000-0000-0000-0000-000000000000',
    GUID: 'ab31cc6e-000f-4e31-8068-372d1b038d3d',
    GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
    Name: 'Sample Node',
    Data: {
      key1: 'value2',
    },
    CreatedUtc: '2024-10-19T14:35:20.351Z',
    Labels: ['test'],
    Tags: {
      Type: 'ActiveDirectory',
    },
    Vectors: [],
    LastUpdateUtc: '2024-10-19T14:35:20.351Z',
  };

  try {
    const updatedNode = await api.Node.update(node);
    console.log(updatedNode, 'Node updated successfully');
  } catch (err) {
    console.log('Error creating node:', JSON.stringify(err));
  }
};

```
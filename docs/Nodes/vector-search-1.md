---
title: Search
excerpt: Perform vector search.
deprecated: false
hidden: false
metadata:
  robots: index
---
To perform vector search call `POST: v1.0/tenants/{tenant-guid}/vectors`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/search' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
  "Ordering": "CreatedDescending",
  "Name": null,
  "Labels": [
    "test"
  ],
  "Tags": {
    "Foo": "Bar"
  },
  "Expr": {
    "Left": "Key",
    "Operator": "Equals",
    "Right": "Value"
  }
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';
import { NodeEdgeSearchRequest  } from 'litegraphdb/dist/types/types';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const searchNodes = async () => {
  const searchRequest: NodeEdgeSearchRequest = {
    GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
    Ordering: 'CreatedDescending',
    Expr: {
      Left: 'Hello',
      Operator: 'Equals',
      Right: 'World',
    },
  };

  try {
    const response = await api.Node.search(searchRequest);
    console.log(response, 'Graph searched successfully');
  } catch (err) {
    console.log('Error searching graph:', JSON.stringify(err), err);
  }
};
```
---
title: Vector Search
excerpt: Perform vector search.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Normal Search

To perform normal search call `POST: v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/search`

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
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/search' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
  "Ordering": "CreatedDescending",
const searchEdges = async () => {
  const searchRequest = {
    GraphGUID: '<graph-guid>',
    Ordering: 'CreatedDescending',
    Expr: {
      Left: 'Hello',
      Operator: 'Equals',
      Right: 'World',
    },
  };

  try {
    const response = await api.Edge.search(searchRequest);
    console.log(response, 'Graph searched successfully');
  } catch (err) {
    console.log('Error searching graph:', JSON.stringify(err), err);
  }
};
```

## Vector Search

To perform vector search call `POST: v1.0/tenants/{tenant-guid}/vectors`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "Domain": "Edge",
    "SearchType": "CosineSimliarity",
    "Labels": [],
    "Tags": {},
    "Expr": null,
    "Embeddings": [ 0.1, 0.2, 0.3 ]
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';
import { NodeEdgeSearchRequest  } from 'litegraphdb/dist/types/types';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const edgeVectorSearch = async () => {
  try {
    const data = await api.Vector.search({
    GraphGUID: "<graph-guid>",
    Domain: "Edge",
    SearchType: "CosineSimliarity",
    Labels: [],
    Tags: {},
    Expr: null,
    Embeddings: [ 0.1, 0.2, 0.3 ]
});
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

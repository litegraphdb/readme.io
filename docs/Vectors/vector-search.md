---
title: Vector Search
excerpt: Perform vector search.
deprecated: false
hidden: false
metadata:
  robots: index
---
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

const vectorSearch = async () => {
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

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
    "SearchType": "CosineSimilarity",
    "Labels": [],
    "Tags": {},
    "Expr": null,
    "Embeddings": [ 0.1, 0.2, 0.3 ]
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";
import { NodeEdgeSearchRequest } from "litegraphdb/dist/types/types";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const edgeVectorSearch = async () => {
  try {
    const data = await api.Vector.search({
      GraphGUID: "<graph-guid>",
      Domain: "Edge",
      SearchType: "CosineSimilarity",
      Labels: [],
      Tags: {},
      Expr: null,
      Embeddings: [0.1, 0.2, 0.3],
    });
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

```json
[
  {
    "Score": 1,
    "Edge": {
      "TenantGUID": "00000000-0000-0000-0000-000000000000",
      "GUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
      "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
      "Name": "My test edge",
      "From": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
      "To": "b9ccf229-f36b-4f1f-98b1-a0e8a4373f71",
      "Cost": 10,
      "CreatedUtc": "2025-09-09T10:03:46.978477Z",
      "LastUpdateUtc": "2025-09-09T10:03:46.978477Z",
      "Data": {
        "Hello": "World"
      },
      "Vectors": [
        {
          "GUID": "8d4d08e6-8bc1-4fe3-9f7f-3a98e38958f0",
          "TenantGUID": "00000000-0000-0000-0000-000000000000",
          "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
          "EdgeGUID": "a1d61bb1-f990-4b90-885c-a925a1cede9d",
          "Model": "all-MiniLM-L6-v2",
          "Dimensionality": 384,
          "Content": "test",
          "Vectors": [0.1, 0.2, 0.3],
          "CreatedUtc": "2025-09-09T10:03:46.979820Z",
          "LastUpdateUtc": "2025-09-09T10:03:46.979820Z"
        }
      ]
    }
  }
]
```

---
title: Get edges from node
excerpt: Get all edges oroginating from node.
deprecated: false
hidden: false
metadata:
  robots: index
---
To find all route between nodes call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges/from`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/1f56dc61-55d3-48e3-b4a9-d54b864f1763/edges/from' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getEdgesFromNode = async () => {
  try {
    const data = await api.Route.getEdgesFromNode(graphGuid, nodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

### Response

```json
[
    {
        "TenantGUID": "00000000-0000-0000-0000-000000000000",
        "GUID": "35dc5401-b17d-4725-abea-5b60654b1f73",
        "GraphGUID": "00000000-0000-0000-0000-000000000000",
        "Name": "ew",
        "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
        "To": "3e991338-d247-4811-80d6-bf54be601686",
        "Cost": 0,
        "CreatedUtc": "2025-08-21T13:23:27.028795Z",
        "LastUpdateUtc": "2025-08-21T13:23:27.028795Z"
    },
    {
        "TenantGUID": "00000000-0000-0000-0000-000000000000",
        "GUID": "2beebc8c-b28d-4605-bfdd-ab80b72087e4",
        "GraphGUID": "00000000-0000-0000-0000-000000000000",
        "Name": "dfg",
        "From": "1f56dc61-55d3-48e3-b4a9-d54b864f1763",
        "To": "64058009-3ff7-40e0-b6d8-02252137fb55",
        "Cost": 0,
        "CreatedUtc": "2025-08-21T13:22:51.591976Z",
        "LastUpdateUtc": "2025-08-21T13:22:51.591976Z"
    }
]
```
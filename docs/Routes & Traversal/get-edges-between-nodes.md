---
title: Get edges between nodes
excerpt: Get all edges between nodes
deprecated: false
hidden: false
metadata:
  robots: index
---
To get all edges between nodes. call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/between?from=<from-node-guid>&to=<to-node-guid>`

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/between?from=00000000-0000-0000-0000-000000000000&to=00000000-0000-0000-0000-000000000001' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getEdgesBetween = async () => {
  try {
    const data = await api.Route.getEdgesBetween(graphGuid, fromNodeGuid, toNodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```
---
title: Exist
deprecated: false
hidden: false
metadata:
  robots: index
---
To check if node exist call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const checkIfEdgeExistsById = async () => {
  try {
    const data = await api.Edge.exists(guid, edgeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
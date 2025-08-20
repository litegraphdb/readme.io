---
title: Export
excerpt: Export a graph in gexf string
deprecated: false
hidden: false
metadata:
  robots: index
---
To export a graph in gexf string call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/export/gexf`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/export/gexf?incldata=null' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const exportGraphToGexf = async () => {
  try {
    const data = await api.Graph.exportGexf('00900db5-c9b7-4631-b250-c9e635a9036e');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
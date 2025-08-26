---
title: Vector Index
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read Configuration

read the configuration of the vectorIndex call ``

```curl
curl --location --request GET 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/vectorindex/config' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readVectorIndexConfig = async () => {
  try {
    const data = await api.Graph.readVectorIndexConfig(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

<br />

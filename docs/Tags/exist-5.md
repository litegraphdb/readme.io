---
title: Exist
excerpt: Check if tag exist.
deprecated: false
hidden: false
metadata:
  robots: index
---
To check if tag exist call `PUT: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const existsTag = async () => {
  try {
    const data = await api.Tag.exists('51e84292-8be4-468e-b9af-5e44c10dc551');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
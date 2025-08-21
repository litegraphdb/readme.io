---
title: Exist
excerpt: Check if label exist.
deprecated: false
hidden: false
metadata:
  robots: index
---
To check if label exist call `PUT: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/','<Tenant-Guid>', '*******');

const existsLabel = async () => {
  try {
    const data = await api.Label.exists('48cee235-5be0-4197-b67f-a9183c7f52b2');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
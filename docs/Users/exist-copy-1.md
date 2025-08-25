---
title: 'Exist '
excerpt: To check if given user exist by id.
deprecated: false
hidden: false
metadata:
  robots: index
---
To check if a user exist call `HEAD: /v1.0/tenants/{tenant-guid}/users/{user-guid}`

```curl
curl --location --head 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const tenantExists = async () => {
  try {
    const data = await api.Tenant.exists('<user-guid>');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

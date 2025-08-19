---
title: Delete
excerpt: To delete a tenant.
deprecated: false
hidden: false
metadata:
  robots: index
---
### Delete

To delete tenant call `DELETE: /v1.0/tenants/{tenant-guid}`

```curl
curl --location --request DELETE 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete('029b9092-3a4c-4f5e-8527-b1b947494e32');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Delete Forcefully

To delete forcefully. pass `force=null` in query parameters.

```curl
curl --location --request DELETE 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000?force=null' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin' \
--data ''
```
```javascript
const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete('029b9092-3a4c-4f5e-8527-b1b947494e32', true);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
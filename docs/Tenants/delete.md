---
title: Delete
excerpt: >-
  Delete a tenant object.  Each tenant is a separate, isolated domain of data
  within LiteGraph.  Tenant APIs require use of the LiteGraph administrative
  bearer token.
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
--header 'Authorization: Bearer ********' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete('<tenant-guid>');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Delete Forcefully

To delete forcefully, pass `?force` in the URL query parameters.

```curl
curl --location --request DELETE 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000?force' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data ''
```
```javascript
const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete('<tenant-guid>', true);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

---
title: Delete
excerpt: Deleting existing user.
deprecated: false
hidden: false
metadata:
  robots: index
---
To delete existing user `DELTE: /v1.0/tenants/{tenant-guid}/users/{user-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer *********' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteUser = async () => {
  try {
    const data = await api.User.delete('8ac86e7e-5612-4193-95d6-2f217dbaeedf');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
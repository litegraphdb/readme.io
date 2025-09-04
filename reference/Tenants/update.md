---
title: Update
excerpt: >-
  Updating tenant objects.  Each tenant is a separate, isolated domain of data
  within LiteGraph.  Tenant APIs require use of the LiteGraph administrative
  bearer token.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update a tenant, call `PUT: /v1.0/tenants/{tenant-guid}`

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "Updated tenant",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateTenant = async () => {
  try {
    const data = await api.Tenant.update({
      GUID: '<tenant-guid>',
      Name: 'Updated tenant',
      Active: true,
      CreatedUtc: '2024-12-27T18:12:38.653402Z',
      LastUpdateUtc: '2024-12-27T18:12:38.653402Z',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

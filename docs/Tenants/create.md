---
title: Create
excerpt: Creating tenats.
deprecated: false
hidden: false
metadata:
  robots: index
---
To create tenants call: `PUT /v1.0/tenants`

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin' \
--data '{
    "Name": "Another tenant",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createTenant = async () => {
  try {
    const created = await api.Tenant.create({
      Name: 'Another tenant',
      Active: true,
    });
    console.log(created);
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Payload properties

* **`Name`** - The display name of the tenant. This is required.
* **`Active`** - A boolean flag indicating whether the tenant should be active (`true`) or inactive (`false`) upon creation. Defaults to `true` if not specified.
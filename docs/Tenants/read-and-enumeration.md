---
title: Read and Enumeration
deprecated: false
hidden: false
metadata:
  robots: index
---
When reading a tenant, use the following structure:

```curl
curl --location --request GET 'http://view.homedns.org:8701/v1.0/tenants/<Tenant-GUID>' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer litegraphadmin'
```

```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readTenant = async () => {
  try {
    const tenant = await api.Tenant.get('<Tenant-GUID>');
    console.log(tenant);
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Response properties

- **`GUID`** - A globally unique identifier for the tenant, represented as a UUID string.
- **`Name`** - The display name of the tenant.
- **`Active`** - A boolean flag indicating whether the tenant is currently active (`true`) or inactive (`false`).
- **`CreatedUtc`** - The date and time (in UTC) when the tenant was initially created.
- **`LastUpdateUtc`** - The date and time (in UTC) when the tenant object was last updated.
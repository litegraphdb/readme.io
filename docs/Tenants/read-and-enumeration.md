---
title: Read and Enumeration
deprecated: false
hidden: false
metadata:
  robots: index
---
## Read

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

<br />

## Enumeration
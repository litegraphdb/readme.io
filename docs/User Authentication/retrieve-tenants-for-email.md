---
title: Retrieve tenants for email
excerpt: Retrieve the list of tenants in which an email address exists.
deprecated: false
hidden: false
metadata:
  robots: index
---
When authenticating using user credentials, you must also include the GUID of the tenant within which you wish to generate a security token on behalf of the user.

To retrieve the list of tenants that hold a user based on a given email address, call `GET /v1.0/token/tenants`

```curl
curl --location --request GET 'http://localhost:8701/v1.0/token/tenants' \
--header 'x-email: default@user.com'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getTenantsForEmail = async () => {
  try {
    const data = await api.Authentication.getTenantsForEmail('user@example.com');
    console.log(data, 'Tenants retrieved successfully');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

<br />

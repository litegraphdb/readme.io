---
title: Generate Auth Token
excerpt: Generate authentication token
deprecated: false
hidden: false
metadata:
  robots: index
---
To generate authentication token (using password), call `GET /v1.0/token`

```curl
curl --location --request GET 'http://localhost:8701/v1.0/token' \
--header 'x-email: default@user.com' \
--header 'x-password: password' \
--header 'x-tenant-guid: 00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const generateToken = async () => {
  try {
    const data = await api.Authentication.generateToken(
      'user@example.com',
      'password123',
      '00000000-0000-0000-0000-000000000000'
    );
    console.log(data, 'Token generated successfully');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

<br />

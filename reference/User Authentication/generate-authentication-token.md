---
title: Generate Authentication Token
excerpt: Generate authentication token using email address, password, and tenant GUID.
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
--header 'x-tenant-guid: 00000000-0000-0000-0000-000000000000'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const generateToken = async () => {
  try {
    const data = await api.Authentication.generateToken(
      'user@example.com',
      'pass****',
      '<tenanat-guid>'
    );
    console.log(data, 'Token generated successfully');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def generate_authentication_token():
    token = litegraph.Authentication.generate_authentication_token(email="user@example.com", password="pass****", tenant_guid="tenanat-guid")
    print(token)
    
generate_authentication_token()

```

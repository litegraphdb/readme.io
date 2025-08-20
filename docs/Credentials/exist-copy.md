---
title: Exist
excerpt: To check if given credential exist by id.
deprecated: false
hidden: false
metadata:
  robots: index
---
To check if a credential exist call `HEAD : /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`

```curl
curl --location --head 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const existsCredential = async () => {
  try {
    const data = await api.Credential.exists('fba86eda-21ea-4095-852c-5f5c542f0ffc');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
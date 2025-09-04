---
title: Delete
excerpt: Delete existing credential.
deprecated: false
hidden: false
metadata:
  robots: index
---
To delete existing credential call `DELETE: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteCredential = async () => {
  try {
    const data = await api.Credential.delete('<credential-guid>');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

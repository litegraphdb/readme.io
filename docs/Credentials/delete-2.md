---
title: Delete
excerpt: Delete existing credential.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing credential call `PUT: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "UserGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Updated credential",
    "BearerToken": "default",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateCredential = async () => {
  try {
    const data = await api.Credential.update({
      UserGUID: 'a2b230c7-c57f-4194-b042-1333102226b1',
      Name: 'Updated credential',
      BearerToken: 'default',
      Active: true,
      LastUpdateUtc: '2024-12-27T18:12:38.653402Z',
      CreatedUtc: '2024-12-27T18:12:38.653402Z',
      GUID: 'fba86eda-21ea-4095-852c-5f5c542f0ffc',
      TenantGUID: '',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```
---
title: Create
excerpt: Create a credential.
deprecated: false
hidden: false
metadata:
  robots: index
---
To create credential call `PUT: /v1.0/tenants/{tenant-guid}/credentials`

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "UserGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "New credential",
    "BearerToken": "foobar",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const createCredential = async () => {
  try {
    const data = await api.Credential.create({
      UserGUID: '<user-guid>',
      Name: 'New credential',
      BearerToken: 'foobar',
      Active: true,
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

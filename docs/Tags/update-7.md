---
title: Update
excerpt: Update existing tags.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing tag call `PUT: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Key": "updatedkey",
    "Value": "myvalue"
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateTag = async () => {
  try {
    const data = await api.Tag.update({
      GraphGUID: '00900db5-c9b7-4631-b250-c9e635a9036e',
      NodeGUID: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
      EdgeGUID: '53b94bd9-98ea-47e6-9e5a-4fe346298717',
      Key: 'updatedkey',
      Value: 'myvalue',
      CreatedUtc: '2024-12-27T18:12:38.653402Z',
      LastUpdateUtc: '2024-12-27T18:12:38.653402Z',
      GUID: '51e84292-8be4-468e-b9af-5e44c10dc551',
      TenantGUID: '',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};


```
---
title: Update
excerpt: Update existing labels.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing edge call `PUT: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Label": "updatedlabel"
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateLabel = async () => {
  try {
    const data = await api.Label.update({
      GUID: '48cee235-5be0-4197-b67f-a9183c7f52b2',
      GraphGUID: '5de4ba59-cd38-4ed5-a4cc-09b2532e65b2',
      NodeGUID: 'dce18cf8-6443-4d14-b4a3-c72dcc28d6d8',
      Label: 'updatedkey',
      EdgeGUID: 'e9702f09-cd73-413b-8e00-5f871472a02d',
      CreatedUtc: '2024-12-27T18:12:38.653402Z',
      LastUpdateUtc: '2024-12-27T18:12:38.653402Z',
      TenantGUID: '',
    });
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```
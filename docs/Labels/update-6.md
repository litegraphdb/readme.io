---
title: Update
excerpt: Update existing labels.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing label call `PUT: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

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
      GUID: guid,
      GraphGUID: '<graph-guid>',
      NodeGUID: '<node-guid>',
      Label: 'updatedkey',
      EdgeGUID: '<edge-guid>',
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

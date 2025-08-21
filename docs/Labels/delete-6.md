---
title: Delete
excerpt: Delete existing label.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single label

To delete existing label call `DELETE: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteLabel = async () => {
  try {
    const data = await api.Label.delete('48cee235-5be0-4197-b67f-a9183c7f52b2');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete multiple labels

To delete multiple labels call `DELETE: /v1.0/tenants/{tenant-guid}/labels/bulk`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteMultipleLabels = async () => {
  try {
    const data = await api.Label.deleteBulk([
      '23513268-7fe7-4867-ab3e-c7a5dc4b2e57',
      '9f8d49e0-031a-4de0-b643-ce48dc3774fe',
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
---
title: Delete
excerpt: Delete existing label.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single label

To delete existing edge call `DELETE: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`

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

To delete multiple edges call `DELETE: /v1.0/tenants/{tenant-guid}/labels/bulk`

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

const deleteMultipleEdges = async () => {
  try {
    const data = await api.Edge.deleteBulk('00900db5-c9b7-4631-b250-c9e635a9036e', [
      '934c11b3-61df-4fc5-972c-6e9d0ee3aa19',
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
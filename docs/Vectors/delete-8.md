---
title: Delete
excerpt: Delete existing vectors.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single vector

To delete existing vector call `DELETE: /v1.0/tenants/{tenant-guid}/vectors/{vector-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteVector = async () => {
  try {
    const data = await api.Vector.delete('<vector-guid>');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete multiple vectors

To delete multiple vectors call `DELETE: /v1.0/tenants/{tenant-guid}/vectors/bulk`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/vectors/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteMultipleVectors = async () => {
  try {
    const data = await api.Vector.deleteBulk([vector-guid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

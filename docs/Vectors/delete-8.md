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
    const data = await api.Vector.delete('70cd93dd-0f38-435d-b57d-f5d1bc1b4481');
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
    const data = await api.Vector.deleteBulk([
      '64ee007a-14f5-43b0-99a0-9a22fb4a24b9',
      '9823faa0-a8ae-4479-a87d-56cf18d27696',
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
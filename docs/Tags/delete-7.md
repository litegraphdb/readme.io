---
title: Delete
excerpt: Delete existing tag.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single tag

To delete existing tag call `DELETE: /v1.0/tenants/{tenant-guid}/tags/{tag-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteTag = async () => {
  try {
    const data = await api.Tag.delete('51e84292-8be4-468e-b9af-5e44c10dc551');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```

## Delete multiple labels

To delete multiple edges call `DELETE: /v1.0/tenants/{tenant-guid}/tags/bulk`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteMultipleTags = async () => {
  try {
    const data = await api.Tag.deleteBulk([
      '5ab74644-888b-4215-90ba-23a01b1fdbe3',
      'd842fa4b-163f-4edd-85b1-df38facb9bed',
    ]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
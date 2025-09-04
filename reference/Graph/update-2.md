---
title: Delete
excerpt: Delete existing  graph.
deprecated: false
hidden: false
metadata:
  robots: index
next:
  pages:
    - slug: running-server-from-binary
      title: Running Server from Source
      type: basic
---
To delete graph call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteGraphById = async () => {
  try {
    const data = await api.Graph.delete(guid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

### Delete forcefull

To delete graph call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}?force`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000?force=null' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteGraphById = async () => {
  try {
    const data = await api.Graph.delete(guid, true);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

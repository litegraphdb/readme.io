---
title: Exist
excerpt: Check if node exist.
deprecated: false
hidden: false
metadata:
  robots: index
---
To  check if edge exists call `HEAD: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`

```curl
curl --location --request HEAD 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteEdgeById = async () => {
  try {
    const data = await api.Edge.delete(guid, edgeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};

```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    graph_guid="Graph-Guid",
    access_key="******",
)

def exists_edge():
    exists = litegraph.Edge.exists(guid="edge-guid")
    print(exists)

exists_edge()
```

<br />

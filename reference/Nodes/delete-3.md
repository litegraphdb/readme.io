---
title: Delete
excerpt: Delete existing node.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Delete single node

To delete existing node call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteNodeById = async () => {
  try {
    const data = await api.Node.delete(guid, nodeGuid);
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
    graph-guid="Graph-Guid",
    access_key="******",
)

def delete_node():
    litegraph.Node.delete(guid="node-guid")
    print("Node deleted")
    
delete_node()

```

## Delete multiple node

To delete multiple nodes call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteMultipleNodes = async () => {
  try {
    const data = await api.Node.deleteBulk(grapGuid, [node-guid]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};

```

## Delete all nodes

To delete existing node call `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/all`

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/all' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const deleteAllNodes = async () => {
  try {
    const data = await api.Node.deleteAll(<graph-guid>);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```

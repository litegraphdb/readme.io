---
title: Get node edges
excerpt: Get all edges of a node
deprecated: false
hidden: false
metadata:
  robots: index
---
To get all edges of a node. call `GET: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}/edges`

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000/edges' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getAllNodeEdges = async () => {
  try {
    const data = await api.Route.getAllNodeEdges(graphGuid, nodeGuid);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err), err);
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    access_key="******",
)

def get_edges_of_node():
    edges = litegraph.RouteNodes.edges(
        graph_guid="graph-guid",
        node_guid="node-guid"
    )
    print(edges)

get_edges_of_node()
```

<br />

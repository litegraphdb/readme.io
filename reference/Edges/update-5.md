---
title: Update
excerpt: Update existing edge.
deprecated: false
hidden: false
metadata:
  robots: index
---
To update existing edge call `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "Updated",
    "From": "5ad4b899-9b2b-430c-8ebb-8623a49959ae",
    "To": "0b739acf-8e1d-40d9-86e7-5a4d18cb501d",
    "Cost": 100,
    "Labels": [
        "test",
        "updated"
    ],
    "Tags": {
        "type": "edge",
        "test": "true",
        "updated": "true"
    },
    "Data": {
        "Hello": "World",
        "Foo": "Bar"
    }
}'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const updateEdge = async () => {
  const edge: Edge = {
    TenantGUID: '<tenant-guid>',
    GUID: guid,
    GraphGUID: '<graph-guid>',
    Name: 'My test edge',
    From: '<from-node-guid>',
    To: '<to-node-guid>',
    Cost: 10,
    Data: {
      Hello: 'World',
    },
    CreatedUtc: '2024-07-01 15:43:06.991834',
    Labels: ['test'],
    Tags: {
      Type: 'ActiveDirectory',
    },
    Vectors: [],
    LastUpdateUtc: '2024-07-01 15:43:06.991834',
  };

  try {
    const createdEdge = await api.Edge.update(edge);
    console.log(createdEdge, 'Edge updated successfully');
  } catch (err) {
    console.log('Error updating edge:', JSON.stringify(err));
  }
};

```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    graph_guid="Graph-Guid"
    access_key="******",
)

def update_edge():
    edge = litegraph.Edge.update(guid="edge-guid",name="My test edge",cost=10)
    print(edge)

update_edge()
```

<br />

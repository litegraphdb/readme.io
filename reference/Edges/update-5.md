---
title: Update Edge
excerpt: >-
  Comprehensive guide for updating existing edges, including modifying edge
  properties, updating metadata, and handling edge modifications with proper
  validation and error handling for effective edge management.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Edge update operations allow you to modify existing edges within your graph database. This functionality is essential for maintaining data accuracy, correcting edge properties, and adapting edge information as your application requirements evolve. Understanding edge update operations is crucial for effective edge management and ensuring your graph structure remains current and relevant.

Key capabilities include:

* Updating edge names, properties, and metadata
* Modifying edge relationships and connections
* Maintaining data integrity during updates
* Handling validation and error scenarios
* Preserving edge relationships and associations

These operations support various use cases such as edge refinement, metadata updates, data correction, and maintaining consistency across your graph database.

## Update Edge

Update an existing edge using `PUT: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/edges/{edge-guid}`. This endpoint allows you to modify the edge properties, relationships, and metadata of a specific edge while preserving its unique identifier and maintaining its associations with nodes.

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
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateEdge = async () => {
  const edge = {
    TenantGUID: "<tenant-guid>",
    GUID: guid,
    GraphGUID: "<graph-guid>",
    Name: "My test edge",
    From: "<from-node-guid>",
    To: "<to-node-guid>",
    Cost: 10,
    Data: {
      Hello: "World",
    },
    CreatedUtc: "2024-07-01 15:43:06.991834",
    Labels: ["test"],
    Tags: {
      Type: "ActiveDirectory",
    },
    Vectors: [],
    LastUpdateUtc: "2024-07-01 15:43:06.991834",
  };

  try {
    const createdEdge = await api.Edge.update(edge);
    console.log(createdEdge, "Edge updated successfully");
  } catch (err) {
    console.log("Error updating edge:", JSON.stringify(err));
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

def update_edge():
    edge = litegraph.Edge.update(guid="edge-guid", name="My test edge", cost=10)
    print(edge)

update_edge()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;
using System.Collections.Specialized;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
Edge response = liteGraph.Edge.Update(new Edge()
{
    Name = "My test edge",
    From = Guid.Parse("<from-node-guid>"),
    To = Guid.Parse("<to-node-guid>"),
    Cost = 10,
    Labels = new List<string> { "test", "hello" },
    Tags = new NameValueCollection
    {
        { "type", "edge" },
        { "test", "true" }
    },
    Data = new
    {
        Hello = "World"
    }
});

```

### Response

Upon successful edge update, the API returns a `200 OK` status code with the updated edge object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Updated",
  "From": "5ad4b899-9b2b-430c-8ebb-8623a49959ae",
  "To": "0b739acf-8e1d-40d9-86e7-5a4d18cb501d",
  "Cost": 100,
  "Labels": ["test", "updated"],
  "Tags": {
    "type": "edge",
    "test": "true",
    "updated": "true"
  },
  "Data": {
    "Hello": "World",
    "Foo": "Bar"
  },
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```

## Best Practices

When updating edges, consider the following recommendations:

* **Validate Data**: Always validate edge properties before sending update requests
* **Preserve Relationships**: Ensure updates don't break existing node associations
* **Handle Conflicts**: Implement proper handling for concurrent update scenarios
* **Backup Before Updates**: Consider backing up critical edge data before major updates
* **Monitor Changes**: Track edge modifications for audit and debugging purposes
* **Use Atomic Operations**: Ensure updates are atomic to maintain data consistency
* **Test Updates**: Validate update operations in development environments first

## Next Steps

After successfully updating edges, consider these next actions:

* **Verify Changes**: Read the updated edge to confirm changes were applied correctly
* **Update Dependencies**: Check if any dependent systems need to be notified of changes
* **Monitor Impact**: Track how edge updates affect related operations and queries
* **Document Changes**: Maintain documentation of edge modification history
* **Optimize Performance**: Review update patterns for potential performance improvements

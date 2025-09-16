---
title: Update Label
excerpt: >-
  Comprehensive guide for updating existing labels, including modifying label
  names, updating metadata, and handling label modifications with proper
  validation and error handling for effective label management.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Label update operations allow you to modify existing labels within your graph database. This functionality is essential for maintaining data accuracy, correcting label names, and adapting label information as your application requirements evolve. Understanding label update operations is crucial for effective label management and ensuring your label system remains current and relevant.

Key capabilities include:

* Updating label names and properties
* Modifying label metadata and associations
* Maintaining data integrity during updates
* Handling validation and error scenarios
* Preserving label relationships and associations

These operations support various use cases such as label refinement, metadata updates, data correction, and maintaining consistency across your graph database.

## Update Label

Update an existing label using `PUT: /v1.0/tenants/{tenant-guid}/labels/{label-guid}`. This endpoint allows you to modify the label name and other properties of a specific label while preserving its unique identifier and maintaining its associations with nodes or edges.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Label": "updatedlabel"
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateLabel = async () => {
  try {
    const data = await api.Label.update({
      GUID: guid,
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      Label: "updatedkey",
      EdgeGUID: "<edge-guid>",
      CreatedUtc: "2024-12-27T18:12:38.653402Z",
      LastUpdateUtc: "2024-12-27T18:12:38.653402Z",
      TenantGUID: "",
    });
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
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

def update_label():
    label = litegraph.Label.update(guid="label-guid",label="Updated Label")
    print(label)

update_label()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
LabelMetadata response = liteGraph.Label.Update(new LabelMetadata()
{
    GraphGUID = Guid.Parse("<graph-guid>"),
    NodeGUID = Guid.Parse("<node-guid>"),
    EdgeGUID = Guid.Parse("<edge-guid>"),
    Label = "updatedlabel",
});
```

### Response

Upon successful label update, the API returns a `200 OK` status code with the updated label object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": null,
  "EdgeGUID": null,
  "Label": "updatedlabel",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:15:42.123456Z"
}
```

## Best Practices

When updating labels, consider the following recommendations:

* **Validate Data**: Always validate label names before sending update requests
* **Preserve Relationships**: Ensure updates don't break existing node or edge associations
* **Handle Conflicts**: Implement proper handling for concurrent update scenarios

## Next Steps

After successfully updating labels, consider these next actions:

* **Verify Changes**: Read the updated label to confirm changes were applied correctly
* **Update Dependencies**: Check if any dependent systems need to be notified of changes
* **Monitor Impact**: Track how label updates affect related operations and queries
* **Document Changes**: Maintain documentation of label modification history
* **Optimize Performance**: Review update patterns for potential performance improvements

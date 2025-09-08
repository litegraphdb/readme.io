---
title: Create Label
excerpt: >-
  Comprehensive guide for creating individual labels and performing bulk label
  creation operations, including label management, categorization, and efficient
  label storage for effective graph organization and data classification.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Label creation operations enable you to create and manage labels within your graph database. Labels are essential for organizing, categorizing, and classifying nodes and edges in your graph structure. Understanding label creation is crucial for building well-organized graph databases and implementing effective data classification systems.

Key capabilities include:

* Creating individual labels with custom names and associations
* Performing bulk label creation for efficient batch processing
* Associating labels with specific nodes or edges in your graph
* Managing label metadata and properties for organization
* Supporting hierarchical and categorical data structures

These operations support various use cases such as data classification, graph organization, content categorization, and implementing custom data taxonomies.

## Create Single Label

Create a single label using `PUT: /v1.0/tenants/{tenant-guid}/labels`. This endpoint allows you to create a new label with a specific name and associate it with nodes or edges in your graph for effective data organization and classification.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label"
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createLabel = async () => {
  try {
    const data = await api.Label.create({
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      Label: "test",
      EdgeGUID: null,
    });
    console.log(data, "chk data");
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

def create_label():
    label = litegraph.Label.create(graph_guid="graph-guid",label="test")
    print(label)

create_label()
```

### Response

Upon successful label creation, the API returns a `201 Created` status code with the created label object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": null,
  "EdgeGUID": null,
  "Label": "label",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Create Multiple Labels

Create multiple labels in a single operation using `PUT: /v1.0/tenants/{tenant-guid}/labels/bulk`. This bulk operation allows you to efficiently create multiple labels with different names and associations in one API call, which is useful for batch labeling operations and data organization.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/labels/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label"
  }
]''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createMultipleLabels = async () => {
  try {
    const data = await api.Label.createBulk([
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Label: "label multiple",
      },
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Label: "label multiple 2",
      },
    ]);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

### Response

Upon successful bulk label creation, the API returns a `201 Created` status code with an array of created label objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Label": "label",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Next Steps

After successfully creating labels, consider these next actions:

* **Update Labels**: Modify existing labels using the update operations
* **Delete Labels**: Remove unnecessary labels to maintain data cleanliness
* **Create New Labels**: Add additional labels based on your analysis
* **Integrate Data**: Use created labels in your application logic
* **Monitor Usage**: Track label usage patterns for optimization opportunities

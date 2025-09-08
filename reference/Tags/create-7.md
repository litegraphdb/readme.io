---
title: Create Tag
excerpt: >-
  Create single or multiple tags for nodes and edges with key-value pairs to
  enhance graph metadata and enable advanced filtering and categorization.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Create Tag endpoints allow you to add metadata tags to nodes and edges within your graph. This functionality is essential for:

* Adding key-value metadata to graph elements
* Enabling advanced filtering and search capabilities
* Categorizing and organizing graph data
* Supporting both single tag and bulk tag creation operations
* Enhancing graph analytics and reporting
* Implementing custom data classification systems

## Request Parameters

The tag creation request accepts the following properties:

### Tag Properties

* **GraphGUID**: The graph's unique identifier (string, required)
* **NodeGUID**: The node's unique identifier to tag (string, optional - null if tagging an edge)
* **EdgeGUID**: The edge's unique identifier to tag (string, optional - null if tagging a node)
* **Key**: The tag key/name (string, required)
* **Value**: The tag value (string, required)

### System Properties (Read-only)

* **GUID**: The tag's unique identifier (string, auto-generated)
* **TenantGUID**: The tenant's unique identifier (string, auto-assigned)
* **CreatedUtc**: Timestamp when the tag was created (string, auto-generated)
* **LastUpdateUtc**: Timestamp of last update (string, auto-generated)

**Note**: GUID, TenantGUID, CreatedUtc, and LastUpdateUtc are automatically managed by the system. Either NodeGUID or EdgeGUID must be specified, but not both.

## Create Single Tag

Create a single tag using `PUT: /v1.0/tenants/{tenant-guid}/tags`. This endpoint allows you to add a key-value pair tag to a specific node or edge within a graph.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue"
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createTag = async () => {
  try {
    const data = await api.Tag.create({
      GraphGUID: "<graph-guid>",
      NodeGUID: "<node-guid>",
      EdgeGUID: "<edge-guid>",
      Key: "mykey",
      Value: "myvalue",
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

def create_tag():
    tag = litegraph.Tag.create(key="mykey",value="myvalue")
    print(tag)

create_tag()
```

### Response

Upon successful tag creation, the API returns a `201 Created` status code with the created tag object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": "00000000-0000-0000-0000-000000000001",
  "EdgeGUID": null,
  "Key": "mykey",
  "Value": "myvalue",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Create Multiple Tags

Create multiple tags in a single operation using `PUT: /v1.0/tenants/{tenant-guid}/tags/bulk`. This bulk operation allows you to efficiently create multiple tags with different key-value pairs in one API call, which is useful for batch tagging operations and data organization.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
  {
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": null,
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue"
  }
]'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const createMultipleTags = async () => {
  try {
    const data = await api.Tag.createBulk([
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Key: "mykey test",
        Value: "myvalue test",
      },
      {
        GraphGUID: "<graph-guid>",
        NodeGUID: "<node-guid>",
        EdgeGUID: "<edge-guid>",
        Key: "mykey test 2",
        Value: "myvalue test 2",
      },
    ]);
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

def create_multiple_tag():
    tags = litegraph.Tag.create_multiple(tags=[
        {
            "Key": "Test Key 1",
            "Value": "Test Value 1"
        },
        {
            "Key": "Test Key 2",
            "Value": "Test Value 2"
        }
    ])
    print(tags)

create_multiple_tag()

```

### Response

Upon successful bulk tag creation, the API returns a `201 Created` status code with an array of created tag objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000002",
    "EdgeGUID": null,
    "Key": "mykey test",
    "Value": "myvalue test",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000003",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000002",
    "EdgeGUID": null,
    "Key": "mykey test 2",
    "Value": "myvalue test 2",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Best Practices

When creating tags, consider the following recommendations:

1. **Use Descriptive Keys**: Choose clear, meaningful key names for better organization
2. **Consistent Naming**: Establish naming conventions for tag keys across your graph
3. **Bulk Operations**: Use bulk creation for multiple tags to improve performance
4. **Validate Data**: Always validate tag key-value pairs before sending requests

## Next Steps

After successfully creating tags, you can:

* Use tags for advanced filtering in search and enumeration operations
* Build tag-based analytics and reporting features
* Implement tag management interfaces for users
* Create tag-based access control and permissions
* Set up automated tag validation and cleanup processes
* Build tag visualization and exploration tools
* Implement tag-based recommendation systems
* Create tag usage analytics and monitoring dashboards

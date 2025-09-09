---
title: Delete Node
excerpt: Delete single, multiple, or all nodes from a graph with proper relationship handling and data integrity preservation.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Delete Node endpoints allow you to remove nodes from a graph with different levels of granularity. This functionality is essential for:

- Removing individual nodes that are no longer needed
- Bulk deletion of multiple nodes for cleanup operations
- Complete graph reset by deleting all nodes
- Maintaining graph integrity during deletion operations
- Implementing node lifecycle management
- Cleaning up test data and temporary nodes

## Delete Single Node

Remove a specific node from the graph using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/{node-guid}`. This endpoint allows you to delete a single node by its unique identifier while maintaining graph integrity.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteNodeById = async () => {
  try {
    const data = await api.Node.delete(guid, nodeGuid);
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
    graph-guid="Graph-Guid",
    access_key="******",
)

def delete_node():
    litegraph.Node.delete(guid="node-guid")
    print("Node deleted")

delete_node()

```

## Delete Multiple Nodes

Remove multiple specific nodes from the graph using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/bulk`. This bulk operation allows you to efficiently delete multiple nodes by providing their GUIDs in a single API call, which is useful for cleanup operations and batch processing.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/bulk' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '[
    "00000000-0000-0000-0000-000000000000"
]'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteMultipleNodes = async () => {
  try {
    const data = await api.Node.deleteBulk(grapGuid, [node - guid]);
    console.log(data, "check data");
  } catch (err) {
    console.log("err:", JSON.stringify(err), err);
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

def delete_multiple_node():
    litegraph.Node.delete_multiple(guid=["node-guid","node-guid-1"])
    print("Nodes deleted")

delete_multiple_node()

```

## Delete All Nodes

Remove all nodes from the graph using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}/nodes/all`. This operation completely clears the graph of all nodes and is typically used for graph reset operations, testing cleanup, or when starting fresh with a new dataset.

**Warning**: This operation is irreversible and will delete all nodes in the graph. Use with extreme caution in production environments.

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
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="Tenant-Guid",
    graph-guid="Graph-Guid",
    access_key="******",
)

def delete_all_node():
    litegraph.Node.delete_all()
    print("Nodes deleted")

delete_all_node()
```

## Response

Upon successful deletion, the API returns a `200 OK` status code. The response varies depending on the deletion operation:

## Best Practices

When deleting nodes, consider the following recommendations:

1. **Backup Critical Data**: Always backup important nodes before deletion operations
2. **Check Dependencies**: Verify that deleting nodes won't break graph relationships
3. **Use Bulk Operations**: Use bulk deletion for multiple nodes to improve performance

## Next Steps

After successfully deleting nodes, you can:

- Verify the deletion by attempting to read the deleted nodes
- Clean up any orphaned edges that may have been connected to deleted nodes
- Update dependent systems that may have referenced the deleted nodes
- Implement node deletion notifications for affected users
- Create deletion audit reports and compliance documentation
- Set up automated cleanup processes for temporary nodes
- Build node lifecycle management interfaces
- Implement data retention policies and automated deletion schedules

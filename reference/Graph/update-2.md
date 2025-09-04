---
title: Delete Graph
excerpt: Delete existing graphs with standard or force deletion options, including all associated nodes, edges, and data.
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

## Overview

The Delete Graph endpoints allow you to permanently remove graphs from your tenant. When you delete a graph, all associated nodes, edges, vectors, and custom data are also removed. The API provides two deletion modes:

- **Standard Delete**: Performs a standard deletion with safety checks
- **Force Delete**: Bypasses safety checks for immediate deletion

**Warning**: Graph deletion is irreversible. All data associated with the graph will be permanently lost.

## Standard Delete

Remove a graph using the standard deletion process with `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}`. This method includes safety checks to prevent accidental deletion of graphs with active dependencies.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000' \
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

const deleteGraphById = async () => {
  try {
    const data = await api.Graph.delete(guid);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Force Delete

Force delete a graph by bypassing safety checks using `DELETE: /v1.0/tenants/{tenant-guid}/graphs/{graph-guid}?force`. This method immediately removes the graph and all associated data without performing dependency checks.

**Use with caution**: Force delete should only be used when you need to immediately remove a graph that may have dependencies or when standard deletion fails due to constraint violations.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000?force=null' \
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

const deleteGraphById = async () => {
  try {
    const data = await api.Graph.delete(guid, true);
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Response

Upon successful deletion, the API returns a `204 No Content` status code, indicating that the graph has been successfully removed. No response body is returned for successful deletions.

## Best Practices

When deleting graphs, consider the following recommendations:

1. **Verify Dependencies**: Check if the graph has any dependent nodes or edges before deletion
2. **Use Standard Delete First**: Always try standard deletion before resorting to force delete
3. **Backup Important Data**: Consider backing up critical data before deletion
4. **Confirm Graph Selection**: Double-check the graph GUID to ensure you're deleting the correct graph
5. **Monitor Dependencies**: Be aware of any applications or processes that might depend on the graph

## Next Steps

After successfully deleting a graph, you can:

- Create new graphs to replace deleted ones
- Review remaining graphs in your tenant
- Clean up any orphaned references in your application
- Update any dependent systems that referenced the deleted graph

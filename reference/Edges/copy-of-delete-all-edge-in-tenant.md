---
title: Copy of Delete All Edge In Tenant
excerpt: >-
  Delete all edges within a specific tenant. This is a bulk deletion operation
  that removes all edge records for the specified tenant GUID.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Delete All Edge In Tenant` endpoint allows you to delete all edges associated with a tenant. This operation is useful when performing a complete cleanup of edges within a tenant or when resetting the graph structure without affecting the tenant's other data (such as nodes). The operation ensures that all edge relationships are removed and associated data is cleaned up.

**Important:** This operation requires administrative privileges. Once the edges are deleted, the operation is irreversible, and all relationships and associated data will be lost.

Key capabilities include:

* Deleting all edges within a tenant.
* Cleaning up edge relationships and associated data.
* Optimizing storage by removing obsolete or unnecessary edges
* Maintaining graph integrity while performing cleanup.

## Delete All Edge In Tenant

Delete all edges within a tenant using the following `DELETE request:
DELETE: /v1.0/tenants/{tenant-guid}/edges/all`
This operation removes all edge records for the specified tenant GUID, permanently deleting all relationships within that tenant.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",  
  "*******"  
);

const EdgeDeleteAllInTenant = async () => {
  try {
    const data = await api.Edge.deleteAllInTenant();  
    console.log(data, 'All edges in tenant deleted');
  } catch (err) {
    console.log('Error:', JSON.stringify(err));
  }
};
```

## Response

Upon successful edge deletion, the API returns a **200 No Content** status code, indicating that all edges have been successfully removed from the system. No response body is returned for successful deletions.

* **200 No Content:** All edges in the specified tenant have been successfully deleted.
* **401 Unauthorized:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant does not exist.

## Best Practices

When deleting edges, consider the following recommendations:

* **Verify Before Deletion**: Always confirm the edges you intend to delete are correct
* **Backup Important Data**: Consider backing up critical edge data before deletion
* **Check Dependencies**: Ensure no critical systems depend on the edges being deleted
* **Use Bulk Operations**: Leverage bulk deletion for multiple edges to improve performance
* **Handle Errors Gracefully**: Implement proper error handling for failed deletions
* **Monitor Impact**: Track the effects of edge deletions on related operations
* **Maintain Audit Trail**: Keep records of deletion operations for compliance and debugging

## Next Steps

After successfully deleting edges, consider these next actions:

* **Verify Deletion**: Confirm edges have been removed by attempting to read them
* **Update Dependencies**: Check if any dependent systems need to be updated
* **Clean Up References**: Remove any local references to deleted edges
* **Monitor System**: Watch for any issues that might arise from the deletions
* **Document Changes**: Maintain documentation of deletion operations
* **Optimize Storage**: Review storage usage improvements from the cleanup
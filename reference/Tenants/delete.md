---
title: Delete Tenant
excerpt: >-
  Delete tenant objects with isolated data domains within LiteGraph using
  administrative bearer token authentication, with optional force deletion.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Delete Tenant endpoint allows you to permanently remove tenant objects from your LiteGraph instance. When you delete a tenant, all associated data including graphs, nodes, edges, and vectors are also permanently removed. This functionality provides:

* Complete tenant removal and cleanup
* Data isolation and security enforcement
* Administrative control over tenant lifecycle
* Force deletion capabilities for problematic tenants

**Warning**: Tenant deletion is irreversible. All data associated with the tenant will be permanently lost.

**Important**: Tenant deletion requires administrative privileges and must use the LiteGraph administrative bearer token for authentication.

## Delete Tenant

Remove a tenant using the standard deletion process with `DELETE: /v1.0/tenants/{tenant-guid}`. This method includes safety checks to prevent accidental deletion of tenants with active dependencies or data.

```curl
curl --location --request DELETE 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete("<tenant-guid>");
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

def delete_tenant():
    litegraph.Tenant.delete(guid="tenant-guid")
    print("Tenant deleted")

delete_tenant()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

public static class Example
{
    public static async Task Main(string[] args)
    {
        LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
        liteGraph.InitializeRepository();
        liteGraph.Tenant.DeleteByGuid(Guid.Parse("<tenant-guid>"));
    }
}
```

## Delete Forcefully

Force delete a tenant by bypassing safety checks using `DELETE: /v1.0/tenants/{tenant-guid}?force`. This method immediately removes the tenant and all associated data without performing dependency checks.

**Use with caution**: Force delete should only be used when you need to immediately remove a tenant that may have dependencies or when standard deletion fails due to constraint violations.

```curl
curl --location --request DELETE 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000?force' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data ''
```
```javascript
const deleteTenant = async () => {
  try {
    const data = await api.Tenant.delete("<tenant-guid>", true);
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

def delete_tenant_force():
    litegraph.Tenant.delete(guid="tenant-guid", force=True)
    print("Tenant deleted")

delete_tenant_force()

```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

public static class Example
{
    public static async Task Main(string[] args)
    {
        LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
        liteGraph.InitializeRepository();
        liteGraph.Tenant.DeleteByGuid(Guid.Parse("<tenant-guid>"), force: true);
    }
}
```

## Response

Upon successful deletion, the API returns a `200 No Content` status code, indicating that the tenant has been successfully removed. No response body is returned for successful deletions.

## Best Practices

When deleting tenants, consider the following recommendations:

1. **Verify Dependencies**: Check if the tenant has any dependent data or active users before deletion
2. **Use Standard Delete First**: Always try standard deletion before resorting to force delete
3. **Backup Important Data**: Consider backing up critical data before deletion
4. **Confirm Tenant Selection**: Double-check the tenant GUID to ensure you're deleting the correct tenant
5. **Monitor Dependencies**: Be aware of any applications or processes that might depend on the tenant

## Next Steps

After successfully deleting a tenant, you can:

* Clean up any orphaned references in your application
* Update any dependent systems that referenced the deleted tenant
* Review remaining tenants in your system
* Implement tenant lifecycle management policies
* Update your tenant management documentation

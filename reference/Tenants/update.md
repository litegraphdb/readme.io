---
title: Update Tenant
excerpt: >-
  Update existing tenant objects with modified properties and configuration
  using administrative bearer token authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Update Tenant endpoint allows you to modify existing tenant objects within your LiteGraph instance. This functionality enables you to update tenant properties such as name, active status, and other configuration settings. This is essential for:

* Modifying tenant display names and descriptions
* Activating or deactivating tenants

**Important**: Tenant updates require administrative privileges and must use the LiteGraph administrative bearer token for authentication.

## Update Tenant

Modify an existing tenant using `PUT: /v1.0/tenants/{tenant-guid}` with the updated tenant properties in the request body. This endpoint allows you to update tenant configuration while preserving the tenant's unique identifier and creation timestamp.

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data '{
    "Name": "Updated tenant",
    "Active": true
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const updateTenant = async () => {
  try {
    const data = await api.Tenant.update({
      GUID: "<tenant-guid>",
      Name: "Updated tenant",
      Active: true,
      CreatedUtc: "2024-12-27T18:12:38.653402Z",
      LastUpdateUtc: "2024-12-27T18:12:38.653402Z",
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

def update_tenant():
    tenant = litegraph.Tenant.update(guid="tenant-guid", name="Updated Tenant")
    print(tenant)

update_tenant()

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
        TenantMetadata response = liteGraph.Tenant.Update(new TenantMetadata()
        {
            Name = "Updated tenant",
            Active = true,
        });
    }
}
```

## Request Parameters

The tenant update request supports the following parameters:

* **`GUID`**: The unique identifier of the tenant to update (required)
* **`Name`**: The updated display name of the tenant (optional)
* **`Active`**: The updated active status of the tenant (optional)
* **`CreatedUtc`**: The original creation timestamp (preserved from existing tenant)
* **`LastUpdateUtc`**: The original last update timestamp (will be updated automatically)

## Response

Upon successful update, the API returns a `200 OK` status with the updated tenant object containing:

* **TenantGUID**: The unique identifier of the updated tenant
* **Name**: The updated display name
* **Active**: The updated active status
* **CreatedUtc**: The original creation timestamp (unchanged)
* **LastUpdateUtc**: The new timestamp reflecting when the update occurred

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "Name": "Updated tenant",
  "Active": true,
  "CreatedUtc": "2025-08-29T13:54:54.956041Z",
  "LastUpdateUtc": "2025-09-08T10:00:45.175616Z"
}
```

<br />

## Best Practices

When updating tenants, consider the following recommendations:

1. **Preserve System Fields**: Always include the original CreatedUtc and LastUpdateUtc timestamps
2. **Validate Changes**: Ensure the updated values are valid and consistent
3. **Administrative Access**: Verify you have proper administrative privileges before updating

## Next Steps

After successfully updating a tenant, you can:

* Verify the changes by reading the updated tenant
* Update any dependent systems that reference the tenant
* Implement tenant change notifications and workflows
* Monitor tenant usage and performance after changes
* Update tenant management documentation and records

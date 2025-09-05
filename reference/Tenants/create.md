---
title: Create Tenant
excerpt: >-
  Create new tenant objects with isolated data domains within LiteGraph using
  administrative bearer token authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Create Tenant endpoint allows you to create new tenant objects within your LiteGraph instance. Each tenant represents a separate, isolated domain of data, providing complete data separation and security boundaries. This functionality is essential for:

* Multi-tenant application architectures
* Data isolation and security
* Organizational separation of graph data

**Important**: Tenant creation requires administrative privileges and must use the LiteGraph administrative bearer token for authentication.

## Create Tenant

Create a new tenant using `PUT: /v1.0/tenants` with the LiteGraph administrative API key. This endpoint creates a new isolated data domain with its own graphs, nodes, edges, and associated data.

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data '{
    "Name": "Another tenant",
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

const createTenant = async () => {
  try {
    const created = await api.Tenant.create({
      Name: "Another tenant",
      Active: true,
    });
    console.log(created);
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://192.168.101.63:8701",
    tenant_guid="00000000-0000-0000-0000-000000000000",
    access_key="litegraphadmin",
)

def create_tenant():
    tenant = litegraph.Tenant.create(name="Test Tenant")
    print(tenant)
    
create_tenant()

```

## Request Parameters

The tenant creation request supports the following parameters:

* **`Name`** - The display name of the tenant. This is a required field and should be descriptive and unique within your organization.
* **`Active`** - A boolean flag indicating whether the tenant should be active (`true`) or inactive (`false`) upon creation. Defaults to `true` if not specified. Inactive tenants cannot be used for data operations until they are activated.

## Response

Upon successful creation, the API returns a `201 Created` status with the created tenant object containing:

* **TenantGUID**: The unique identifier assigned to the newly created tenant
* **Name**: The display name provided in the request
* **Active**: The active status of the tenant
* **CreatedUtc**: Timestamp when the tenant was created
* **LastUpdateUtc**: Timestamp of the last update (initially the same as CreatedUtc)

## Best Practices

When creating tenants, consider the following recommendations:

1. **Naming Convention**: Use consistent and descriptive naming conventions for tenant names
2. **Active Status**: Consider creating tenants as inactive initially if you need to configure them before use
3. **Security**: Ensure administrative bearer tokens are properly secured and rotated regularly
4. **Documentation**: Maintain documentation of tenant purposes and ownership
5. **Monitoring**: Implement monitoring for tenant creation and usage patterns

## Next Steps

After successfully creating a tenant, you can:

* Create graphs within the new tenant
* Set up user authentication for the tenant
* Configure tenant-specific settings and permissions
* Begin adding nodes, edges, and data to tenant graphs
* Implement tenant-specific business logic and workflows

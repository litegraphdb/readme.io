---
title: Delete All Credentials In Tenant
excerpt: >-
  Delete all credentials associated with a specific tenant, permanently removing
  all credential records for the specified tenant GUID.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Delete All Credentials In Tenant` endpoint enables the deletion of all credentials associated with a particular tenant. This is a bulk deletion operation and is typically used when:

* You need to remove all credentials for a tenant (e.g., tenant deactivation or complete credential reset).
* Implementing credential cleanup after a breach or other security incident.
* Resetting credentials in the case of a complete system refresh or migration.

**Important:** This operation requires admin-level authentication and will delete **all** credentials for the specified tenant GUID. Deletion is irreversible, and all access associated with the credentials will be immediately revoked.

## Delete All Credentials In Tenant

Permanently delete all credentials for a specific tenant using the following `DELETE request:
DELETE: /v1.0/tenants/{tenant-guid}/credentials`
This endpoint will remove all credential records and revoke access for the specified tenant.

**Authentication:** Admin only (Admin privileges required for access).

**Parameters:** 

* **Tenant GUID (from request context):**  The unique identifier for the tenant whose credentials are being deleted.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",  
  "*******" 
);

const CredentialDeleteAllInTenant = async () => {
  try {
    const data = await api.Credential.deleteAllInTenant();
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Response

Upon successful deletion, the API will return a **200 No Content** status code, indicating that all credentials have been successfully removed. No response body is returned for successful deletions.

* **200 No Content:** All credentials for the tenant have been successfully deleted.
* **401 Unauthorized:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant does not exist.

## Best Practices

When deleting all credentials for a tenant, consider the following security recommendations:

* **Double-Check Tenant GUID:** Ensure the correct tenant GUID is provided to avoid unintended credential deletion.
* **Inform Users:** Notify users whose credentials are being deleted and provide appropriate steps to regain access.
* **Verify Active Credentials:** Review whether any credentials are actively in use before initiating the deletion process.
* **Backups:** Ensure that you have proper backups of credentials or associated data, in case of accidental deletion.

## Next Steps

After successfully deleting all credentials for a tenant, consider the following:

* Set up new credentials for the tenant as needed.
* Ensure all systems that used the deleted credentials are updated with new ones.
* Review and audit the security and usage policies for the tenant to ensure future credentials are managed securely.
* Implement policies to automatically handle credential expiration, rotation, and cleanup in the future.

---
title: Delete Credential By User
excerpt: >-
  Delete all credentials associated with a specific user within a tenant,
  permanently removing all credential records for the specified user GUID.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The `Delete Credential By User` endpoint enables the deletion of all credentials associated with a particular user within a tenant. This is a bulk deletion operation for a specific user and is typically used when:

* Credential cleanup is required for a particular user, either due to security concerns or user role changes.
* Implementing user access control changes, such as when a user is no longer allowed to access certain resources or services.

**Important:** This operation requires admin-level authentication and will delete **all credentials** associated with the specified user within the tenant. Deletion is irreversible, and all access associated with the user's credentials will be immediately revoked.

## Delete Credential By User

Permanently delete all credentials for a specific user within the tenant using the following `DELETE request:
DELETE: /v1.0/tenants/{tenant-guid}/users/{user-guid}/credentials`
This endpoint will remove all credential records associated with the user and revoke all access for that user within the tenant.

**Authentication:** Admin only (Admin privileges required for access).

**Parameters:**

* **Tenant GUID (from request context):**  The unique identifier for the tenant whose credentials are being deleted.
* **User GUID (from request context):** The unique identifier for the user whose credentials are being deleted.

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",  
  "*******" 
);

const CredentialDeleteByUserGuid = async () => {
  try {
    const data = await api.Credential.deleteByUserGuid('<user-guid>');
    console.log(data, 'All credentials for user deleted');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

## Response

Upon successful deletion, the API will return a **200 No Content** status code, indicating that all credentials for the user have been successfully removed. No response body is returned for successful deletions.

* **200 No Content:** All credentials for the specified user have been successfully deleted.
* **401 Unauthorized:** Admin authentication is required to perform this action.
* **404 Not Found:** The specified tenant or user does not exist.

## Best Practices

When deleting credentials by user, consider the following security recommendations:

* **Double-Check User and Tenant GUIDs:** Ensure the correct user and tenant GUIDs are provided to avoid unintended credential deletion.
* **Inform Users:** Notify users whose credentials are being deleted and provide appropriate steps to regain access if necessary.
* **Verify Active Credentials:** Review whether the credentials are actively in use before initiating the deletion process.
* **Backups:** Ensure that you have proper backups of credentials or associated data, in case of accidental deletion.

## Next Steps

After successfully deleting all credentials for a tenant, consider the following:

* Set up new credentials for the user as needed.
* Ensure all systems that used the deleted credentials are updated with new ones.
* Review and audit the security and usage policies for the tenant to ensure future credentials are managed securely.
* Implement policies to automatically handle credential expiration, rotation, and cleanup in the future.

<br />

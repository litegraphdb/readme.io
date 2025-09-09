---
title: Delete User
excerpt: >-
  Delete existing user objects from a tenant, permanently removing user accounts
  and associated data with proper authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Delete User endpoint allows you to permanently remove user objects from a specific tenant. When you delete a user, all associated user data, preferences, and access permissions are also permanently removed. This functionality is essential for:

- Removing inactive or terminated user accounts
- Cleaning up user data for compliance and privacy
- Managing user lifecycle within tenant boundaries
- Implementing user account termination workflows
- Maintaining data security and access control

**Warning**: User deletion is irreversible. All data associated with the user will be permanently lost.

## Delete User

Remove an existing user from a specific tenant using `DELETE: /v1.0/tenants/{tenant-guid}/users/{user-guid}`. This endpoint permanently removes the user account and all associated data from the tenant.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer *********' \
--data ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteUser = async () => {
  try {
    const data = await api.User.delete("<user-guid>");
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

def delete_user():
    litegraph.User.delete(guid="user-guid")
    print("User deleted")

delete_user()
```

## Response

Upon successful deletion, the API returns a `200 No Content` status code, indicating that the user has been successfully removed. No response body is returned for successful deletions.

## Best Practices

When deleting users, consider the following recommendations:

1. **Verify Dependencies**: Check if the user has any dependent data or active sessions before deletion
2. **Backup Important Data**: Consider backing up critical user data before deletion
3. **Confirm User Selection**: Double-check the user GUID to ensure you're deleting the correct user

## Next Steps

After successfully deleting a user, you can:

- Clean up any orphaned references in your application
- Update any dependent systems that referenced the deleted user
- Review remaining users in the tenant

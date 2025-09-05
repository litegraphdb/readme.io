---
title: Update User
excerpt: >-
  Update existing user information including personal details, authentication
  credentials, and account status using the PUT endpoint with proper validation.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Update User endpoint allows you to modify existing user information within a tenant. This functionality is essential for:

* Updating user personal information (name, email)
* Changing user authentication credentials
* Modifying user account status and permissions
* Implementing user profile management features
* Maintaining accurate user data across the system

**Important**: User updates require appropriate permissions within the tenant and must use a valid authentication token. All updates are validated before being applied.

## Update User

Update an existing user's information using `PUT: /v1.0/tenants/{tenant-guid}/users/{user-guid}`. This endpoint allows you to modify user properties including personal details, authentication credentials, and account status.

```curl
curl --location --request PUT 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********' \
--data-raw '{
    "FirstName": "Again Updated",
    "LastName": "User",
    "Email": "anotherbbb@user.com",
    "Password": "password",
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

const updateUser = async () => {
  try {
    const data = await api.User.update({
      GUID: "<user-guid>",
      FirstName: "Again Updated",
      LastName: "User",
      Email: "anotherbbb@user.com",
      Password: "password",
      Active: true,
      CreatedUtc: "2024-12-27T18:12:38.653402Z",
      LastUpdateUtc: "2024-12-27T18:12:38.653402Z",
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

def update_user():
    user = litegraph.User.update(guid="user-guid", first_name="Again Updated", last_name="User")
    print(user)

update_user()
```

## Request Parameters

The update request accepts the following user properties:

* **FirstName**: User's first name (string)
* **LastName**: User's last name (string)
* **Email**: User's email address (string, must be unique within tenant)
* **Password**: User's password (string, will be hashed securely)
* **Active**: Whether the user account is active (boolean)
* **GUID**: User's unique identifier (string, read-only)
* **CreatedUtc**: Timestamp when user was created (string, read-only)
* **LastUpdateUtc**: Timestamp of last update (string, read-only)

## Response

Upon successful update, the API returns a `200 OK` status code with the updated user object in the response body. The response includes all user properties with the updated values and automatically updated timestamps.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "FirstName": "Again Updated",
  "LastName": "User",
  "Email": "anotherbbb@user.com",
  "Password": "password",
  "Active": true,
  "CreatedUtc": "2025-08-29T13:54:55.050579Z",
  "LastUpdateUtc": "2025-09-05T10:35:36.816339Z"
}
```

## Next Steps

After successfully updating a user, you can:

* Verify the update by reading the user data
* Notify the user about changes to their account
* Update any dependent systems that reference the user
* Implement user profile management interfaces
* Set up automated user data synchronization
* Create user update history and audit logs
* Implement user preference and settings management

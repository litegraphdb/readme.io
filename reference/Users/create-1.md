---
title: Create User
excerpt: >-
  Create new user objects within a tenant with authentication credentials,
  personal information, and access control settings.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

The Create User endpoint allows you to create new user objects within a specific tenant. Each user represents an individual who can access and interact with the tenant's data and resources. This functionality is essential for:

- Setting up user authentication and access control
- Managing user accounts within tenant boundaries
- Establishing user permissions and roles
- Creating user profiles with personal information
- Enabling multi-user collaboration within tenants

## Create User

Create a new user within a specific tenant using `PUT: /v1.0/tenants/{tenant-guid}/users` with the user information in the request body. This endpoint creates a new user account with authentication credentials and profile information.

```curl
curl --location --request PUT 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer *********' \
--data-raw '{
    "FirstName": "Another",
    "LastName": "User",
    "Email": "another@user.com",
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

const createUser = async () => {
  try {
    const data = await api.User.create({
      FirstName: "Another",
      LastName: "User",
      Email: "another@user.com",
      Password: "pass****",
      Active: true,
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

def create_user():
    user = litegraph.User.create(email="another@user.com", password="pass****", first_name="Another", last_name="User")
    print(user)

create_user()
```

## Request Parameters

The user creation request supports the following parameters:

- **`FirstName`**: The user's first name (required)
- **`LastName`**: The user's last name (required)
- **`Email`**: The user's email address, used for authentication and communication (required)
- **`Password`**: The user's initial password for authentication (required)
- **`Active`**: A boolean flag indicating whether the user should be active (`true`) or inactive (`false`) upon creation. Defaults to `true` if not specified

## Response

Upon successful creation, the API returns a `201 Created` status with the created user object containing:

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "FirstName": "Default",
  "LastName": "User",
  "Email": "default@user.com",
  "Password": "password",
  "Active": true,
  "CreatedUtc": "2025-08-29T13:54:55.050579Z",
  "LastUpdateUtc": "2025-08-29T13:54:55.050090Z"
}
```

## Best Practices

When creating users, consider the following recommendations:

1. **Password Security**: Ensure passwords meet security requirements
2. **Email Validation**: Verify email addresses are valid and unique within the tenant
3. **Active Status**: Consider creating users as inactive initially if you need to configure them before activation

## Next Steps

After successfully creating a user, you can:

- Set up user roles and permissions within the tenant
- Configure user-specific settings and preferences
- Send welcome emails or notifications to the new user
- Implement user authentication and login workflows
- Begin adding user-specific data and configurations

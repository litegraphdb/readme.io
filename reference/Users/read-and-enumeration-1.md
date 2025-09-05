---
title: Read and Enumerate Users
excerpt: >-
  Read individual users, multiple users by GUIDs, all users, and perform
  advanced enumeration with search capabilities using various API endpoints.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Read and Enumerate Users endpoints provide comprehensive functionality for retrieving user data from a tenant. These endpoints support various retrieval patterns including:

* Reading individual users by their unique identifier
* Reading multiple users simultaneously by providing a list of GUIDs
* Reading all users within a tenant
* Advanced enumeration with pagination and filtering capabilities
* Search-based enumeration with complex query expressions

**Important**: All read operations require appropriate permissions within the tenant and must use a valid authentication token.

## Read Individual User

Read a single user by its unique identifier using `GET: /v1.0/tenants/{tenant-guid}/users/{user-guid}`. This endpoint returns the complete user data including all properties and metadata.

```curl
curl --location --request GET 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readUser = async () => {
  try {
    const data = await api.User.read("<user-guid>");
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

def retrieve_user():
    user = litegraph.User.retrieve(guid="user-guid")
    print(user)

retrieve_user()
```

## Read Multiple Users by GUIDs

Read multiple users simultaneously by providing a comma-separated list of user GUIDs using `GET: /v1.0/tenants/{tenant-guid}/users?guids=<user1-guid>,<user2-guid>`. This endpoint is efficient for retrieving specific users without fetching all users in the tenant.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users?guids=00000000-0000-0000-0000-000000000000%2C00000000-0000-0000-0000-000000000001' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyUsers = async () => {
  try {
    const data = await api.User.readMany([userGuid]);
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

def retrieve_multiple_user():
    users = litegraph.User.retrieve_many(guids=["userGuid","userGuid2"])
    print(users)

retrieve_multiple_user()
```

## Read All Users

Read all users within a tenant using `GET: /v1.0/tenants/{tenant-guid}/users/`. This endpoint returns a complete list of all users in the tenant. Use this endpoint when you need to retrieve all users or when implementing user management interfaces.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllUsers = async () => {
  try {
    const data = await api.User.readAll();
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

def retrieve_all_user():
    users = litegraph.User.retrieve_all()
    print(users)

retrieve_all_user()
```

## Enumeration (GET)

Perform basic enumeration of users using `GET: /v2.0/tenants/{tenant-guid}/users/`. This endpoint provides a simple way to enumerate all users with basic pagination support. The v2.0 API offers improved performance and additional features compared to the v1.0 endpoints.

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateUsers = async () => {
  try {
    const data = await api.User.enumerate();
    console.log(data, "chk data");
  } catch (err) {
    console.log("err:", JSON.stringify(err));
  }
};
```

## Enumeration and Search (POST)

Perform advanced enumeration with search capabilities using `POST: /v2.0/tenants/{tenant-guid}/users/`. This endpoint allows you to filter, sort, and paginate users based on complex criteria including labels, tags, and custom expressions. It's ideal for implementing sophisticated user search and management interfaces.

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/users' \
--data '{
    "Ordering": "CreatedDescending",
    "IncludeData": false,
    "IncludeSubordinates": false,
    "MaxResults": 5,
    "Skip": 0,
    "ContinuationToken": null,
    "Labels": [ ],
    "Tags": { },
    "Expr": { }
}'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateAndSearchUsers = async () => {
  try {
    const data = await api.User.enumerateAndSearch({
      Ordering: "CreatedDescending",
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
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

def enumerate_with_query_user():
    users = litegraph.User.enumerate_with_query(ordering="CreatedDescending",MaxResults=10,Skip=0,IncludeData=True,IncludeSubordinates=True,Expr=litegraph.ExprModel(Left="Name",Operator="Equals",Right="Test"))
    print(users)

enumerate_with_query_user()

```

## Search Parameters

The POST enumeration endpoint supports the following search parameters:

* **Ordering**: Sort order for results (`CreatedAscending`, `CreatedDescending`, `ModifiedAscending`, `ModifiedDescending`)
* **IncludeData**: Whether to include full user data in the response (boolean)
* **IncludeSubordinates**: Whether to include subordinate users (boolean)
* **MaxResults**: Maximum number of results to return (integer)
* **Skip**: Number of results to skip for pagination (integer)
* **ContinuationToken**: Token for continuing pagination from previous request (string)
* **Labels**: Array of label filters to apply (array of strings)
* **Tags**: Object containing tag-based filters (object)
* **Expr**: Complex expression for advanced filtering (object with Left, Operator, Right properties)

## Response

All read and enumeration endpoints return JSON responses containing user data. The response structure varies based on the endpoint:

* **Individual User**: Returns a single user object with all properties
* **Multiple Users**: Returns an array of user objects
* **All Users**: Returns an array of all user objects in the tenant
* **Enumeration**: Returns paginated results with metadata including continuation tokens

## Best Practices

When reading and enumerating users, consider the following recommendations:

1. **Use Appropriate Endpoints**: Choose the right endpoint based on your needs (individual vs. multiple vs. all users)
2. **Implement Pagination**: Use MaxResults and ContinuationToken for large datasets
3. **Optimize Data Retrieval**: Use IncludeData=false when you only need user metadata
4. **Use Search Filters**: Leverage Labels, Tags, and Expr parameters for efficient filtering

## Next Steps

After reading user data, you can:

* Display user information in your application interface
* Implement user management and administration features
* Perform user-specific operations based on retrieved data
* Update user information using the update endpoints
* Implement user search and filtering functionality
* Build user analytics and reporting features
* Integrate user data with other system components

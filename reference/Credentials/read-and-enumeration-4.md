---
title: Read and Enumerate Credentials
excerpt: >-
  Read individual credentials, multiple credentials by GUIDs, all credentials,
  and perform advanced enumeration with search capabilities using various API
  endpoints.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Read and Enumerate Credentials endpoints provide comprehensive functionality for retrieving credential data from a tenant. These endpoints support various retrieval patterns including:

* Reading individual credentials by their unique identifier
* Reading multiple credentials simultaneously by providing a list of GUIDs
* Reading all credentials within a tenant
* Advanced enumeration with pagination and filtering capabilities
* Search-based enumeration with complex query expressions

**Important**: All read operations require appropriate permissions within the tenant and must use a valid authentication token.

## Read Individual Credential

Read a single credential by its unique identifier using `GET: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`. This endpoint returns the complete credential data including all properties and metadata.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readCredential = async () => {
  try {
    const data = await api.Credential.read("<credential-guid>");
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

def retrieve_credential():
    credential = litegraph.Credential.retrieve(guid="credential-guid")
    print(credential)

retrieve_credential()
```

### Response

```json
{
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "UserGUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Default credential",
    "BearerToken": "default",
    "Active": true,
    "CreatedUtc": "2025-08-29T13:54:55.175279Z",
    "LastUpdateUtc": "2025-08-29T13:54:55.174491Z"
}
```

## Read Multiple Credentials by GUIDs

Read multiple credentials simultaneously by providing a comma-separated list of credential GUIDs using `GET: /v1.0/tenants/{tenant-guid}/credentials?guids=<credential1-guid>,<credential2-guid>`. This endpoint is efficient for retrieving specific credentials without fetching all credentials in the tenant.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials?guids=00000000-0000-0000-0000-000000000000%2C00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const readManyCredentials = async () => {
  try {
    const data = await api.Credential.readMany([<credential-guid>]);
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
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

def retrieve_multiple_credential():
    credentials = litegraph.Credential.retrieve_many(guids=["credential-guid","credential-guid2"])
    print(credentials)

retrieve_multiple_credential()
```

## Read All Credentials

Read all credentials within a tenant using `GET: /v1.0/tenants/{tenant-guid}/credentials/`. This endpoint returns a complete list of all credentials in the tenant. Use this endpoint when you need to retrieve all credentials or when implementing credential management interfaces.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllCredentials = async () => {
  try {
    const data = await api.Credential.readAll();
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

def retrieve_all_credential():
    credentials = litegraph.Credential.retrieve_all()
    print(credentials)

retrieve_all_credential()
```

## Enumeration (GET)

Perform basic enumeration of credentials using `GET: /v2.0/tenants/{tenant-guid}/credentials/`. This endpoint provides a simple way to enumerate all credentials with basic pagination support. The v2.0 API offers improved performance and additional features compared to the v1.0 endpoints.

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateCredentials = async () => {
  try {
    const data = await api.Credential.enumerate();
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

def enumerate_credential():
    credentials = litegraph.Credential.enumerate()
    print(credentials)

enumerate_credential()
```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T10:05:20.543278Z",
        "End": "2025-09-08T10:05:20.549982Z",
        "TotalMs": 6.7,
        "Messages": {}
    },
    "MaxResults": 1000,
    "EndOfResults": true,
    "TotalRecords": 1,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "GUID": "00000000-0000-0000-0000-000000000000",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "UserGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Default credential",
            "BearerToken": "default",
            "Active": true,
            "CreatedUtc": "2025-08-29T13:54:55.175279Z",
            "LastUpdateUtc": "2025-08-29T13:54:55.174491Z"
        }
    ]
}
```

## Enumeration and Search (POST)

Perform advanced enumeration with search capabilities using `POST: /v2.0/tenants/{tenant-guid}/credentials`. This endpoint allows you to filter, sort, and paginate credentials based on complex criteria including labels, tags, and custom expressions. It's ideal for implementing sophisticated credential search and management interfaces.

### Search Parameters

The POST enumeration endpoint supports the following search parameters:

* **Ordering**: Sort order for results (`CreatedAscending`, `CreatedDescending`, `ModifiedAscending`, `ModifiedDescending`)
* **IncludeData**: Whether to include full credential data in the response (boolean)
* **IncludeSubordinates**: Whether to include subordinate credentials (boolean)
* **MaxResults**: Maximum number of results to return (integer)
* **Skip**: Number of results to skip for pagination (integer)
* **ContinuationToken**: Token for continuing pagination from previous request (string)
* **Labels**: Array of label filters to apply (array of strings)
* **Tags**: Object containing tag-based filters (object)
* **Expr**: Complex expression for advanced filtering (object with Left, Operator, Right properties)

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/credentials' \
--header 'Content-Type: application/json' \
--header 'Authorization: ••••••' \
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

const enumerateAndSearchCredentials = async () => {
  try {
    const data = await api.Credential.enumerateAndSearch({
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

def enumerate_with_query_credential():
    credentials = litegraph.Credential.enumerate_with_query(ordering="CreatedDescending",MaxResults=10,Skip=0,IncludeData=True,IncludeSubordinates=True,Expr=litegraph.ExprModel(Left="Name",Operator="Equals",Right="Test"))
    print(credentials)

enumerate_with_query_credential()
```

### Response

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T10:05:58.611665Z",
        "End": "2025-09-08T10:05:58.615198Z",
        "TotalMs": 3.53,
        "Messages": {}
    },
    "MaxResults": 5,
    "ContinuationToken": "00000000-0000-0000-0000-000000000000",
    "EndOfResults": false,
    "TotalRecords": 1,
    "RecordsRemaining": 1,
    "Objects": [
        {
            "GUID": "00000000-0000-0000-0000-000000000000",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "UserGUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Default credential",
            "BearerToken": "default",
            "Active": true,
            "CreatedUtc": "2025-08-29T13:54:55.175279Z",
            "LastUpdateUtc": "2025-08-29T13:54:55.174491Z"
        }
    ]
}
```

## Response

All read and enumeration endpoints return JSON responses containing credential data. The response structure varies based on the endpoint:

* **Individual Credential**: Returns a single credential object with all properties
* **Multiple Credentials**: Returns an array of credential objects
* **All Credentials**: Returns an array of all credential objects in the tenant
* **Enumeration**: Returns paginated results with metadata including continuation tokens

## Best Practices

When reading and enumerating credentials, consider the following recommendations:

1. **Use Appropriate Endpoints**: Choose the right endpoint based on your needs (individual vs. multiple vs. all credentials)
2. **Implement Pagination**: Use MaxResults and ContinuationToken for large datasets
3. **Optimize Data Retrieval**: Use IncludeData=false when you only need credential metadata
4. **Handle Errors Gracefully**: Implement proper error handling for different HTTP status codes
5. **Cache Results**: Consider caching frequently accessed credential data
6. **Use Search Filters**: Leverage Labels, Tags, and Expr parameters for efficient filtering
7. **Monitor Performance**: Be aware of the performance impact when reading large numbers of credentials

## Next Steps

After reading credential data, you can:

* Display credential information in your application interface
* Implement credential management and administration features
* Perform credential-specific operations based on retrieved data
* Update credential information using the update endpoints
* Implement credential search and filtering functionality
* Build credential analytics and reporting features
* Integrate credential data with other system components

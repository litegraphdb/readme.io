---
title: Read and Enumerate Tenants
excerpt: >-
  Read individual tenants, retrieve tenant statistics, and enumerate multiple
  tenants with filtering and search capabilities using administrative
  authentication.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Read and Enumeration endpoints provide comprehensive functionality for retrieving tenant data from your LiteGraph instance. These endpoints allow you to:

* Read individual tenants by their unique identifier
* Retrieve tenant statistics and metadata
* Enumerate multiple tenants with various filtering options
* Search and filter tenants based on labels, tags, and custom expressions
* Implement pagination for large result sets

**Important**: All tenant read and enumeration operations require administrative privileges and must use the LiteGraph administrative bearer token for authentication.

## Read Individual Tenant

Retrieve a specific tenant by its unique identifier using `GET: /v1.0/tenants/{tenant-guid}`. This endpoint returns the complete tenant object including all metadata, configuration, and status information.

```curl
curl --location --request GET 'http://view.homedns.org:8701/v1.0/tenants/<Tenant-GUID>' \
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

const readTenant = async () => {
  try {
    const tenant = await api.Tenant.get("<Tenant-GUID>");
    console.log(tenant);
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

def retrieve_tenant():
    tenant = litegraph.Tenant.retrieve(guid="tenanat-guid")
    print(tenant)

retrieve_tenant()

```

### Response 

```json
{
    "GUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Default tenant",
    "Active": true,
    "CreatedUtc": "2025-08-29T13:54:54.956041Z",
    "LastUpdateUtc": "2025-08-29T13:54:54.955375Z"
}
```

## Read Tenant Statistics

Retrieve statistical information about a specific tenant using `GET: /v1.0/tenants/{tenant-id}/stats`. This endpoint provides metrics such as graph count, node count, edge count, and other performance-related statistics for the tenant.

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/stats' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readTenantStatistic = async () => {
  try {
    const data = await api.Tenant.readStatistic(guid);
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

def retrieve_statistics_single_tenant():
    statistics = litegraph.Tenant.retrieve_statistics(tenant_guid="tenanat-guid")
    print(statistics)
    
retrieve_statistics_single_tenant()

```

### Response

```json
{
    "Graphs": 1,
    "Nodes": 0,
    "Edges": 0,
    "Labels": 0,
    "Tags": 0,
    "Vectors": 0
}
```

## Read Multiple Tenants by GUIDs

Retrieve multiple specific tenants by providing their GUIDs as query parameters using `GET: /v1.0/tenants?guids=<tenant1-guid>,<tenant2-guid>`. This endpoint allows you to fetch several tenants in a single request by specifying comma-separated GUIDs in the URL query string.

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants?guids=00000000-0000-0000-0000-000000000000%2C00000000-0000-0000-0000-000000000001' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyTenants = async () => {
  try {
    const data = await api.Tenant.readMany([tenantGuid]);
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

def retrieve_multiple_tenants():
    tenants = litegraph.Tenant.retrieve_many(["Tenant-Guid","Tenant-Guid-2"])
    print(tenants)
    
retrieve_multiple_tenants()

```

## Read All Tenants

Retrieve all tenants within your LiteGraph instance using `GET: /v1.0/tenants`. This endpoint returns a complete list of all tenants, including their metadata and basic information.

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readTenants = async () => {
  try {
    const data = await api.Tenant.readAll();
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

def retrieve_all_tenants():
    tenants = litegraph.Tenant.retrieve_all()
    print(tenants)
    
retrieve_all_tenants()

```

## Read All Tenant Statistics

Retrieve statistical information for all tenants in your LiteGraph instance using `GET: /v1.0/tenants/stats`. This endpoint provides aggregated statistics across all tenants, including total graph counts, node counts, edge counts, and other performance metrics.

```curl
curl --location 'http://view.homedns.org:8701/v1.0/tenants/stats' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllTenantStatistics = async () => {
  try {
    const data = await api.Tenant.readStatistics();
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

def retrieve_statistics_all_tenant():
    statistics = litegraph.Tenant.retrieve_statistics()
    print(statistics)
    
retrieve_statistics_all_tenant()
```

### Response

```json
{
    "00000000-0000-0000-0000-000000000000": {
        "Graphs": 1,
        "Nodes": 0,
        "Edges": 0,
        "Labels": 0,
        "Tags": 0,
        "Vectors": 0
    },
    "1361d1f4-bb3b-409e-9436-528d41e260bf": {
        "Graphs": 0,
        "Nodes": 0,
        "Edges": 0,
        "Labels": 0,
        "Tags": 0,
        "Vectors": 0
    }
}
```

## Enumeration (GET)

The v2.0 enumeration endpoint `GET: /v2.0/tenants` provides enhanced enumeration capabilities with improved response formatting and pagination support. This endpoint is designed for efficient enumeration of large tenant collections with optimized response structures.

```curl
curl --location 'http://view.homedns.org:8701/v2.0/tenants' \
--header 'Authorization: Bearer ********'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateTenants = async () => {
  try {
    const data = await api.Tenant.enumerate();
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

def enumerate_tenant():
    tenants = litegraph.Tenant.enumerate()
    print(tenants)
    
enumerate_tenant()
```

### Response

```json
{
  "Success": true,
  "Timestamp": {
    "Start": "2025-08-14T13:40:37.667042Z",
    "End": "2025-08-14T13:40:37.676703Z",
    "TotalMs": 9.66,
    "Messages": {}
  },
  "MaxResults": 1000,
  "EndOfResults": true,
  "TotalRecords": 1,
  "RecordsRemaining": 0,
  "Objects": [
    {
      "GUID": "00000000-0000-0000-0000-000000000000",
      "Name": "Default tenant",
      "Active": true,
      "CreatedUtc": "2025-01-20T02:51:11.325726Z",
      "LastUpdateUtc": "2025-01-20T02:51:11.325727Z"
    }
  ]
}
```

## Enumeration and Search (POST)

The advanced enumeration endpoint `POST: /v2.0/tenants` provides powerful search and filtering capabilities along with enumeration. This endpoint supports complex query parameters including ordering, pagination, label filtering, tag matching, and custom expressions. It's ideal for applications that need to implement sophisticated tenant discovery and search functionality.

### Search Parameters

The POST request body supports the following parameters:

* **Ordering**: Sort results by creation date (CreatedAscending, CreatedDescending)
* **IncludeData**: Whether to include custom data in the response
* **IncludeSubordinates**: Whether to include subordinate tenant information
* **MaxResults**: Maximum number of results to return (for pagination)
* **Skip**: Number of results to skip (for pagination)
* **ContinuationToken**: Token for continuing pagination from a previous request
* **Labels**: Array of labels to filter tenants
* **Tags**: Key-value pairs for tag-based filtering
* **Expr**: Custom expression for advanced filtering

```curl
curl --location 'http://view.homedns.org:8701/v2.0/tenants' \
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

const enumerateAndSearchTenants = async () => {
  try {
    const data = await api.Tenant.enumerateAndSearch({
      Ordering: "CreatedDescending",
      IncludeData: false,
      IncludeSubordinates: false,
      MaxResults: 5,
      ContinuationToken: null,
      Labels: [],
      Tags: {},
      Expr: {},
    });
    console.log(data);
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

def enumerate_with_query_tenant():
    tenants = litegraph.Tenant.enumerate_with_query(ordering="CreatedDescending",MaxResults=10,Skip=0,IncludeData=True,IncludeSubordinates=True,Expr=litegraph.ExprModel(Left="Name",Operator="Equals",Right="Test"))
    print(tenants)

enumerate_with_query_tenant()

```

### Response 

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T09:59:28.736887Z",
        "End": "2025-09-08T09:59:28.744129Z",
        "TotalMs": 7.24,
        "Messages": {}
    },
    "MaxResults": 5,
    "EndOfResults": true,
    "TotalRecords": 2,
    "RecordsRemaining": 0,
    "Objects": [
        {
            "GUID": "1361d1f4-bb3b-409e-9436-528d41e260bf",
            "Name": "Another tenant",
            "Active": true,
            "CreatedUtc": "2025-09-08T09:53:34.432889Z",
            "LastUpdateUtc": "2025-09-08T09:53:34.432889Z"
        },
        {
            "GUID": "00000000-0000-0000-0000-000000000000",
            "Name": "Default tenant",
            "Active": true,
            "CreatedUtc": "2025-08-29T13:54:54.956041Z",
            "LastUpdateUtc": "2025-08-29T13:54:54.955375Z"
        }
    ]
}
```

## Best Practices

When reading and enumerating tenants, consider the following recommendations:

1. **Administrative Access**: Ensure you have proper administrative privileges before performing operations
2. **Pagination**: Use appropriate pagination parameters for large result sets to optimize performance
3. **Filtering**: Combine enumeration with filtering to reduce unnecessary data transfer

## Next Steps

After reading and enumerating tenants, you can:

* Analyze tenant statistics to understand usage patterns
* Implement tenant management dashboards and monitoring
* Build administrative tools for tenant lifecycle management
* Create tenant-specific configurations and settings
* Implement tenant-based access control and permissions
* Develop tenant migration and backup strategies

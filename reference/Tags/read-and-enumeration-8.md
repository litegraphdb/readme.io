---
title: Read and Enumerate Tags
excerpt: >-
  Comprehensive guide for reading individual tags, retrieving multiple tags by
  GUIDs, reading all tags, and performing enumeration operations with search
  capabilities for efficient tag management and data retrieval.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

Tag reading and enumeration operations provide comprehensive access to tag data within your graph database. These operations enable you to retrieve individual tags, fetch multiple tags by their GUIDs, read all tags in a tenant, and perform advanced enumeration with search capabilities. Understanding these operations is essential for effective tag management, data analysis, and application development.

Key capabilities include:

* Reading individual tags by their unique GUID
* Retrieving multiple specific tags using comma-separated GUIDs
* Reading all tags within a tenant for comprehensive data access
* Enumerating tags with pagination support for large datasets
* Advanced search and filtering capabilities for targeted tag retrieval

These operations support various use cases such as data validation, tag analysis, bulk operations, and integration with external systems that require tag information.

## Read Individual Tag

Read a single tag using `GET: /v1.0/tenants/{tenant-guid}/tags/{tags-guid}`. This endpoint retrieves a specific tag by its unique identifier, providing complete tag information including metadata and timestamps.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readTag = async () => {
  try {
    const data = await api.Tag.read("<tag-guid>");
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

def retrieve_tag():
    tag = litegraph.Tag.retrieve(guid="tag-guid")
    print(tag)

retrieve_tag()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with the tag object in the response body.

```json
{
  "GUID": "00000000-0000-0000-0000-000000000000",
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "GraphGUID": "00000000-0000-0000-0000-000000000000",
  "NodeGUID": "00000000-0000-0000-0000-000000000001",
  "EdgeGUID": null,
  "Key": "mykey",
  "Value": "myvalue",
  "CreatedUtc": "2024-12-27T18:12:38.653402Z",
  "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
}
```

## Read Multiple Tags by GUIDs

Retrieve multiple specific tags using `GET: /v1.0/tenants/{tenant-guid}/tags?guids=<tag1-guid>,<tag2-guid>`. This endpoint allows you to fetch multiple tags in a single request by providing comma-separated GUIDs, which is efficient for retrieving specific tag sets without fetching all tags.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags?guids=00000000-0000-0000-0000-000000000000,00000000-0000-0000-0000-000000000001' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readManyTags = async () => {
  try {
    const data = await api.Tag.readMany([tagGuid]);
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

def retrieve_multiple_tag():
    tags = litegraph.Tag.retrieve_many(guids=["tag-guid","tag-guid-2"])
    print(tags)

retrieve_multiple_tag()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of tag objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000001",
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000002",
    "EdgeGUID": null,
    "Key": "anotherkey",
    "Value": "anothervalue",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Read All Tags

Retrieve all tags within a tenant using `GET: /v1.0/tenants/{tenant-guid}/tags`. This endpoint provides comprehensive access to all tag data in your tenant, useful for data analysis, backup operations, and complete tag inventory management.

```curl
curl --location 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/tags' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const readAllTags = async () => {
  try {
    const data = await api.Tag.readAll();
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

def retrieve_all_tag():
    tags = litegraph.Tag.retrieve_all()
    print(tags)

retrieve_all_tag()
```

### Response

Upon successful retrieval, the API returns a `200 OK` status code with an array of all tag objects in the response body.

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000001",
    "EdgeGUID": null,
    "Key": "mykey",
    "Value": "myvalue",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  },
  {
    "GUID": "00000000-0000-0000-0000-000000000001",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "GraphGUID": "00000000-0000-0000-0000-000000000000",
    "NodeGUID": "00000000-0000-0000-0000-000000000002",
    "EdgeGUID": null,
    "Key": "anotherkey",
    "Value": "anothervalue",
    "CreatedUtc": "2024-12-27T18:12:38.653402Z",
    "LastUpdateUtc": "2024-12-27T18:12:38.653402Z"
  }
]
```

## Enumeration (GET)

Perform tag enumeration using `GET: /v2.0/tenants/{tenant-guid}/tags`. This v2.0 endpoint provides enhanced enumeration capabilities with built-in pagination support, making it ideal for handling large tag datasets efficiently and systematically browsing through tag collections.

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/tags' \
--header 'Authorization: ••••••'
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const enumerateTags = async () => {
  try {
    const data = await api.Tag.enumerate();
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

def enumerate_tag():
    tags = litegraph.Tag.enumerate()
    print(tags)

enumerate_tag()
```

### Response

Upon successful enumeration, the API returns a `200 OK` status code with an array of tag objects and pagination information in the response body.

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T11:17:25.469090Z",
        "End": "2025-09-08T11:17:25.475206Z",
        "TotalMs": 6.12,
        "Messages": {}
    },
    "MaxResults": 1000,
    "ContinuationToken": "ac4b1936-66a2-443b-87a6-396101fc6984",
    "EndOfResults": false,
    "TotalRecords": 4,
    "RecordsRemaining": 4,
    "Objects": [
        {
            "GUID": "8e26e2da-b516-4f0a-ac7d-3a5c8b38721a",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
            "Key": "updated",
            "Value": "true",
            "CreatedUtc": "2025-09-08T10:47:03.877156Z",
            "LastUpdateUtc": "2025-09-08T10:47:03.877163Z"
        },
        {
            "GUID": "62a242b7-d74f-46bc-9677-7a72eb88e61b",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "00000000-0000-0000-0000-000000000000",
            "Key": "updated",
            "Value": "true",
            "CreatedUtc": "2025-09-08T10:46:32.767405Z",
            "LastUpdateUtc": "2025-09-08T10:46:32.767412Z"
        },
        {
            "GUID": "47ef683b-3dc6-45f7-ba75-28475c0615a6",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "Key": "Bar",
            "Value": "Baz",
            "CreatedUtc": "2025-09-08T10:18:03.797402Z",
            "LastUpdateUtc": "2025-09-08T10:18:03.797402Z"
        },
        {
            "GUID": "ac4b1936-66a2-443b-87a6-396101fc6984",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "Key": "Foo",
            "Value": "Bar",
            "CreatedUtc": "2025-09-08T10:18:03.797188Z",
            "LastUpdateUtc": "2025-09-08T10:18:03.797189Z"
        }
    ]
}
```

## Enumeration and Search (POST)

Perform advanced tag enumeration with search capabilities using `POST: /v2.0/tenants/{tenant-guid}/graphs/{graph-guid}/tags`. This powerful endpoint combines enumeration with sophisticated filtering, sorting, and search functionality, allowing you to find specific tags based on various criteria while maintaining efficient pagination for large result sets.

### Search Parameters

The POST endpoint supports various search and filtering parameters:

* **Ordering**: Sort results by creation time (`CreatedAscending`, `CreatedDescending`)
* **IncludeData**: Include full tag data in response (boolean)
* **IncludeSubordinates**: Include related subordinate data (boolean)
* **MaxResults**: Maximum number of results per page (integer)
* **Skip**: Number of results to skip for pagination (integer)
* **ContinuationToken**: Token for continuing pagination (string)
* **Labels**: Filter by specific labels (array)
* **Tags**: Filter by tag key-value pairs (object)
* **Expr**: Advanced expression-based filtering (object)

```curl
curl --location 'http://localhost:8701/v2.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/tags' \
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

const enumerateAndSearchTags = async () => {
  try {
    const data = await api.Tag.enumerateAndSearch({
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

def enumerate_with_query_tag():
    tags = litegraph.Tag.enumerate_with_query(
        ordering="CreatedDescending",
        MaxResults=10,
        Skip=0,
        IncludeData=True,
        IncludeSubordinates=True,
        Expr=litegraph.ExprModel(
            Left="Name",
            Operator="Equals",
            Right="Test"
        )
    )
    print(tags)

enumerate_with_query_tag()
```

### Response

Upon successful enumeration and search, the API returns a `200 OK` status code with filtered tag objects and pagination information in the response body.

```json
{
    "Success": true,
    "Timestamp": {
        "Start": "2025-09-08T11:17:54.248827Z",
        "End": "2025-09-08T11:17:54.252285Z",
        "TotalMs": 3.46,
        "Messages": {}
    },
    "MaxResults": 5,
    "ContinuationToken": "ac4b1936-66a2-443b-87a6-396101fc6984",
    "EndOfResults": false,
    "TotalRecords": 4,
    "RecordsRemaining": 4,
    "Objects": [
        {
            "GUID": "8e26e2da-b516-4f0a-ac7d-3a5c8b38721a",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "72f9cb54-1081-4b6f-a07d-c86d9e0c5150",
            "Key": "updated",
            "Value": "true",
            "CreatedUtc": "2025-09-08T10:47:03.877156Z",
            "LastUpdateUtc": "2025-09-08T10:47:03.877163Z"
        },
        {
            "GUID": "62a242b7-d74f-46bc-9677-7a72eb88e61b",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "00000000-0000-0000-0000-000000000000",
            "Key": "updated",
            "Value": "true",
            "CreatedUtc": "2025-09-08T10:46:32.767405Z",
            "LastUpdateUtc": "2025-09-08T10:46:32.767412Z"
        },
        {
            "GUID": "47ef683b-3dc6-45f7-ba75-28475c0615a6",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "Key": "Bar",
            "Value": "Baz",
            "CreatedUtc": "2025-09-08T10:18:03.797402Z",
            "LastUpdateUtc": "2025-09-08T10:18:03.797402Z"
        },
        {
            "GUID": "ac4b1936-66a2-443b-87a6-396101fc6984",
            "TenantGUID": "00000000-0000-0000-0000-000000000000",
            "GraphGUID": "d913a38a-20fc-4009-a0ec-56229f021885",
            "NodeGUID": "eb787bc5-224b-4551-a70f-9a7eae07a0b8",
            "Key": "Foo",
            "Value": "Bar",
            "CreatedUtc": "2025-09-08T10:18:03.797188Z",
            "LastUpdateUtc": "2025-09-08T10:18:03.797189Z"
        }
    ]
}
```

## Best Practices

When reading and enumerating tags, consider the following recommendations:

* **Use Appropriate Endpoints**: Choose the right endpoint based on your needs (individual read vs. enumeration vs. search)
* **Implement Pagination**: Use MaxResults and ContinuationToken for large datasets to avoid memory issues
* **Optimize Queries**: Use specific GUIDs when possible instead of reading all tags
* **Cache Results**: Implement caching for frequently accessed tag data
* **Handle Errors**: Implement proper error handling for network issues and invalid GUIDs
* **Monitor Performance**: Track response times and optimize queries for better performance
* **Use Search Filters**: Leverage search parameters to reduce data transfer and improve relevance

## Next Steps

After successfully reading and enumerating tags, consider these next actions:

* **Update Tags**: Modify existing tags using the update operations
* **Delete Tags**: Remove unnecessary tags to maintain data cleanliness
* **Create New Tags**: Add additional tags based on your analysis
* **Integrate Data**: Use retrieved tag data in your application logic
* **Monitor Usage**: Track tag usage patterns for optimization opportunities

---
title: Basics
excerpt: >-
  This page covers the basic of interacting with and consuming the LiteGraph
  REST API.
deprecated: false
hidden: false
metadata:
  robots: index
---
## HTTP Methods

LiteGraph primarily uses the following HTTP methods:

* `GET`: Retrieve resources
* `PUT`: Create or update resources
* `POST`: Perform logic operations
* `DELETE`: Remove resources
* `HEAD`: Verify existence of a resource

Note: While these are the general usage patterns, there may be occasional deviations for specific endpoints.

## URL Structure

The general URL structure for the LiteGraph APIs is: `[http||https]://[hostname]:[port]/[apiversion]/tenants/[tenant-guid]/[resource-type]/[resource-guid]`

* `hostname`: Defined by the user based on their deployment
* `port`: Specific to each microservice (see Microservices section).  Most ports are accessible port `8000`
* `apiversion`: In the format `vx.y` (e.g., `v1.0`, `v2.0`)
* `tenant-guid`: Identifies the tenant within the multi-tenant system
* `resource-type`: Specifies the type of resource being accessed
* `resource-guid`: Identifies the individual resource

While this is the typical URL structure, deviations do exist, and will be documented accordingly.

## Authentication

LiteGraph uses three distinct mechanisms for authentication:

* Bearer tokens - used for administrator authentication or for user authentication
* Security tokens - generated via API by passing in credentials and a tenant GUID, security tokens are ephemeral and can be used on subsequent API calls by including them as the value to the `x-token` header

## Response Format

Most LiteGraph APIs return responses in JSON format.

## Error Codes

LiteGraph uses standard HTTP status codes, including:

* `200`: OK
* `201`: Created
* `204`: No Content
* `400`: Bad Request
* `401`: Unauthorized
* `403`: Forbidden
* `404`: Not Found
* `409`: Conflict
* `429`: Too Many Requests
* `500`: Internal Server Error
* `501`: Not Implemented
* `503`: Service Unavailable
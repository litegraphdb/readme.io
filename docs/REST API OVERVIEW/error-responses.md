---
title: Error Responses
excerpt: >-
  This guide documents all API error responses that clients may encounter when
  interacting with LiteGraph Server.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Error Response Structure

All API errors follow a consistent JSON structure:

```json
{
  "Error": "ErrorCode",
  "Message": "Human-readable error message",
  "StatusCode": 400,
  "Context": null,
  "Description": "Optional additional details"
}
```

### Response Fields

| Field         | Type    | Description                                  |
| ------------- | ------- | -------------------------------------------- |
| `Error`       | String  | Error code enum value (see table below)      |
| `Message`     | String  | Human-readable message explaining the error  |
| `StatusCode`  | Integer | HTTP status code                             |
| `Context`     | Object  | Additional contextual information (optional) |
| `Description` | String  | Extra details about the error (optional)     |

## Error Codes Reference

| Error Code             | HTTP Status | Message                                                                                        | Common Causes                                                                                                                        |
| ---------------------- | ----------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `AuthenticationFailed` | 401         | Your authentication material was not accepted.                                                 | Invalid credentials, Missing authentication headers, Expired token, Malformed bearer token                                           |
| `AuthorizationFailed`  | 401         | Your authentication material was accepted, but you are not authorized to perform this request. | Valid credentials but insufficient permissions, Attempting admin operations without admin token, Accessing resources in wrong tenant |
| `BadRequest`           | 400         | We were unable to discern your request. Please check your URL, query, and request body.        | Malformed JSON, Missing required fields, Invalid URL parameters, Incorrect HTTP method                                               |
| `Conflict`             | 409         | Operation failed as it would create a conflict with an existing resource.                      | Creating resource with duplicate GUID, Unique constraint violation, Resource already exists                                          |
| `DeserializationError` | 400         | Your request body was invalid and could not be deserialized.                                   | Invalid JSON syntax, Type mismatch in request body, Unexpected fields in payload                                                     |
| `Inactive`             | 401         | Your account, credentials, or the requested resource are marked as inactive.                   | User account disabled, Credential deactivated, Tenant marked inactive                                                                |
| `InternalError`        | 500         | An internal error has been encountered.                                                        | Database connection failure, Unexpected server exception, Configuration error                                                        |
| `InvalidRange`         | 400         | An invalid range has been supplied and cannot be fulfilled.                                    | Invalid pagination parameters, Out of bounds array indices, Invalid date ranges                                                      |
| `InUse`                | 409         | The requested resource is in use.                                                              | Attempting to delete referenced node, Removing user with active sessions, Deleting tenant with resources                             |
| `NotEmpty`             | 400         | The requested resource is not empty.                                                           | Deleting graph with nodes/edges, Removing tenant with users, Deleting non-empty directory                                            |
| `NotFound`             | 404         | The requested resource was not found.                                                          | Invalid GUID, Resource doesn't exist, Wrong tenant context, Deleted resource                                                         |
| `TooLarge`             | 413         | The size of your request exceeds the maximum allowed by this server.                           | Request body too large, Too many nodes/edges in batch, File upload exceeds limit                                                     |

## Common Error Scenarios

### Authentication Errors

#### Invalid Credentials

**Request:**

```bash
curl -H "x-email: wrong@user.com" \
     -H "x-password: wrongpassword" \
     -H "x-tenant-guid: 00000000-0000-0000-0000-000000000000" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

**Response:**

```json
{
  "Error": "AuthenticationFailed",
  "Message": "Your authentication material was not accepted.",
  "StatusCode": 401,
  "Context": null,
  "Description": "Invalid email or password"
}
```

#### Expired Token

**Request:**

```bash
curl -H "x-token: expired-token-here" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

**Response:**

```json
{
  "Error": "AuthenticationFailed",
  "Message": "Your authentication material was not accepted.",
  "StatusCode": 401,
  "Context": null,
  "Description": "Token has expired"
}
```

### Authorization Errors

#### Insufficient Permissions

**Request:**

```bash
# Regular user attempting admin operation
curl -X PUT \
     -H "Authorization: Bearer user-token" \
     -H "Content-Type: application/json" \
     -d '{"Name": "New Tenant"}' \
     http://localhost:8701/v1.0/tenants
```

**Response:**

```json
{
  "Error": "AuthorizationFailed",
  "Message": "Your authentication material was accepted, but you are not authorized to perform this request.",
  "StatusCode": 401,
  "Context": null,
  "Description": "Admin privileges required"
}
```

### Bad Request Errors

#### Invalid JSON

**Request:**

```bash
curl -X PUT \
     -H "Authorization: Bearer default" \
     -H "Content-Type: application/json" \
     -d '{"Name": "Test", invalid json}' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

**Response:**

```json
{
  "Error": "DeserializationError",
  "Message": "Your request body was invalid and could not be deserialized.",
  "StatusCode": 400,
  "Context": null,
  "Description": "Invalid JSON at position 18"
}
```

#### Missing Required Fields

**Request:**

```bash
curl -X PUT \
     -H "Authorization: Bearer default" \
     -H "Content-Type: application/json" \
     -d '{}' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/edges
```

**Response:**

```json
{
  "Error": "BadRequest",
  "Message": "We were unable to discern your request. Please check your URL, query, and request body.",
  "StatusCode": 400,
  "Context": null,
  "Description": "Required fields are missing"
}
```

### Conflict Errors

#### Duplicate Resource

**Request:**

```bash
curl -X PUT \
     -H "Authorization: Bearer default" \
     -H "Content-Type: application/json" \
     -d '{"GUID": "00000000-0000-0000-0000-000000000000", "Name": "Duplicate"}' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

**Response:**

```json
{
  "Error": "Conflict",
  "Message": "Operation failed as it would create a conflict with an existing resource.",
  "StatusCode": 409,
  "Context": null,
  "Description": "A graph with this GUID already exists"
}
```

### Not Found Errors

#### Invalid Resource GUID

**Request:**

```bash
curl -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/invalid-guid-here
```

**Response:**

```json
{
  "Error": "NotFound",
  "Message": "The requested resource was not found.",
  "StatusCode": 404,
  "Context": null,
  "Description": "Graph not found"
}
```

### Resource In Use Errors

#### Deleting Referenced Node

**Request:**

```bash
curl -X DELETE \
     -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/00000000-0000-0000-0000-000000000000/nodes/node-with-edges
```

**Response:**

```json
{
  "Error": "InUse",
  "Message": "The requested resource is in use.",
  "StatusCode": 409,
  "Context": null,
  "Description": "Cannot delete node with existing edges"
}
```

### Not Empty Errors

#### Deleting Non-Empty Graph

**Request:**

```bash
curl -X DELETE \
     -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs/graph-with-nodes
```

**Response:**

```json
{
  "Error": "NotEmpty",
  "Message": "The requested resource is not empty.",
  "StatusCode": 400,
  "Context": null,
  "Description": "Graph contains nodes and edges. Use ?force to delete"
}
```

## HTTP Status Code Summary

| Status Code | Error Types                                              | Meaning                                |
| ----------- | -------------------------------------------------------- | -------------------------------------- |
| **400**     | BadRequest, DeserializationError, InvalidRange, NotEmpty | Client error - bad request             |
| **401**     | AuthenticationFailed, AuthorizationFailed, Inactive      | Authentication/authorization required  |
| **404**     | NotFound                                                 | Resource doesn't exist                 |
| **409**     | Conflict, InUse                                          | Operation conflicts with current state |
| **413**     | TooLarge                                                 | Request entity too large               |
| **500**     | InternalError                                            | Server error                           |

## Debugging Tips

1. **Check the Description field** - Often contains specific details about what went wrong
2. **Examine the Context object** - May include additional information like conflicting GUIDs or counts
3. **Review HTTP status codes** - Quickly identify the error category
4. **Enable debug logging** - Set `Debug.Exceptions` to `true` in `litegraph.json` for detailed server logs
5. **Validate JSON** - Use a JSON validator before sending requests
6. **Check authentication** - Ensure tokens haven't expired and credentials are correct
7. **Verify GUIDs** - Confirm all GUIDs in the request path and body are valid
8. **Test with curl** - Eliminate client-side issues by testing with curl first

## Rate Limiting and Throttling

While not explicitly defined in the error enum, be aware that the server may return:

* **429 Too Many Requests** - If rate limiting is implemented
* **503 Service Unavailable** - If the server is overloaded

Always implement appropriate backoff strategies for these scenarios.
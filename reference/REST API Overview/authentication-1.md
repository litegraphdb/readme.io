---
title: Authentication
excerpt: >-
  This guide explains the authentication mechanisms available in LiteGraph
  Server and how to use them effectively.
deprecated: false
hidden: false
metadata:
  robots: index
---

## Overview

LiteGraph Server supports three primary authentication methods:

1. **Administrator Bearer Token** - For administrative operations
2. **User Credentials** - Email/password authentication for regular users
3. **Security Tokens** - Temporal tokens for session-based authentication

## Authentication Methods

### 1. Administrator Bearer Token

The administrator bearer token provides full access to all LiteGraph APIs, including administrative functions.

#### Configuration

Set the admin token in `litegraph.json`:

```json
{
  "LiteGraph": {
    "AdminBearerToken": "litegraphadmin"
  }
}
```

#### Usage

Include the token in the `Authorization` header:

```bash
curl -H "Authorization: Bearer litegraphadmin" \
     http://localhost:8701/v1.0/tenants
```

#### Capabilities

- Full access to all APIs
- Tenant management
- User management
- Credential management
- Database backup operations
- System administration functions

#### Security Considerations

- **Change the default token immediately** in production
- Use a strong, randomly generated token
- Rotate the token periodically
- Never expose the admin token in client-side code
- Store securely using environment variables or secrets management

### 2. User Credentials

Regular users authenticate using email, password, and tenant GUID.

#### Default User

On first run, LiteGraph creates a default user:

- **Email**: `default@user.com`
- **Password**: `password`
- **Tenant GUID**: `00000000-0000-0000-0000-000000000000`

#### Authentication Headers

Use three headers for credential-based authentication:

```bash
curl -H "x-email: default@user.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: 00000000-0000-0000-0000-000000000000" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

#### Creating New Users

Only administrators can create new users:

```bash
curl -X PUT \
     -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{
       "FirstName": "John",
       "LastName": "Doe",
       "Email": "john.doe@example.com",
       "Password": "SecurePassword123!",
       "Active": true
     }' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users
```

#### Limitations

- Cannot perform administrative operations
- Access limited to assigned tenant
- Cannot create or modify users
- Cannot manage credentials for other users

### 3. Bearer Token Credentials

Users can have associated bearer tokens for API access without exposing passwords.

#### Default Credential

LiteGraph creates a default credential on first run:

- **Bearer Token**: `default`
- **User GUID**: `00000000-0000-0000-0000-000000000000`

#### Usage

```bash
curl -H "Authorization: Bearer default" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

#### Creating Credentials

Administrators can create bearer token credentials:

```bash
curl -X PUT \
     -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{
       "UserGUID": "00000000-0000-0000-0000-000000000000",
       "Name": "API Access Token",
       "BearerToken": "custom-api-token-123",
       "Active": true
     }' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials
```

#### Benefits

- No need to expose user passwords
- Can create multiple tokens per user
- Tokens can be individually revoked
- Ideal for application integration

### 4. Security Tokens (Temporal Authentication)

Security tokens are time-limited authentication tokens valid for 24 hours.

#### Token Generation

##### Step 1: Find Tenant (if unknown)

If you don't know the tenant GUID:

```bash
curl -H "x-email: default@user.com" \
     http://localhost:8701/v1.0/token/tenants
```

Response:

```json
[
  {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Default tenant",
    "Active": true,
    "CreatedUtc": "2025-02-06T18:22:56.789353Z",
    "LastUpdateUtc": "2025-02-06T18:22:56.788994Z"
  }
]
```

##### Step 2: Generate Token

```bash
curl -H "x-email: default@user.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: 00000000-0000-0000-0000-000000000000" \
     http://localhost:8701/v1.0/token
```

Response:

```json
{
  "TimestampUtc": "2025-01-30T22:54:41.963425Z",
  "ExpirationUtc": "2025-01-31T22:54:41.963426Z",
  "IsExpired": false,
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "UserGUID": "00000000-0000-0000-0000-000000000000",
  "Token": "mXCNtMWDsW0/pr+IwRFUje2n5Z9/qDGprgAY26bz4KYo...",
  "Valid": true
}
```

##### Step 3: Use Token

```bash
curl -H "x-token: mXCNtMWDsW0/pr+IwRFUje2n5Z9/qDGprgAY26bz4KYo..." \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs
```

#### Token Validation

Check if a token is still valid:

```bash
curl -H "x-token: mXCNtMWDsW0/pr+IwRFUje2n5Z9/qDGprgAY26bz4KYo..." \
     http://localhost:8701/v1.0/token/details
```

Response:

```json
{
  "TimestampUtc": "2025-01-30T14:54:41.963425Z",
  "ExpirationUtc": "2025-01-31T14:54:41.963426Z",
  "IsExpired": false,
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "UserGUID": "00000000-0000-0000-0000-000000000000",
  "Valid": true
}
```

#### Benefits

- Time-limited access (24 hours)
- No permanent credential storage needed
- Ideal for web applications
- Automatic expiration
- Can be validated before use

## Authentication Priority

When multiple authentication methods are provided, LiteGraph evaluates them in this order:

1. Administrator bearer token
2. Security token (x-token)
3. User credentials (x-email, x-password, x-tenant-guid)
4. Bearer token credentials

## API Access by Authentication Type

| API Category          | Admin Token | User Credentials | Bearer Token | Security Token |
| --------------------- | ----------- | ---------------- | ------------ | -------------- |
| Tenant Management     | ✅          | ❌               | ❌           | ❌             |
| User Management       | ✅          | ❌               | ❌           | ❌             |
| Credential Management | ✅          | ❌               | ❌           | ❌             |
| Graph Operations      | ✅          | ✅               | ✅           | ✅             |
| Node Operations       | ✅          | ✅               | ✅           | ✅             |
| Edge Operations       | ✅          | ✅               | ✅           | ✅             |
| Vector Operations     | ✅          | ✅               | ✅           | ✅             |
| Backup Operations     | ✅          | ❌               | ❌           | ❌             |
| Database Flush        | ✅          | ❌               | ❌           | ❌             |

## Security Best Practices

### Initial Setup

1. **Change all defaults immediately:**

```bash
# Change admin token in litegraph.json
{
  "LiteGraph": {
    "AdminBearerToken": "your-secure-random-token-here"
  }
}
```

2. **Update default user password:**

```bash
curl -X PUT \
     -H "Authorization: Bearer litegraphadmin" \
     -H "Content-Type: application/json" \
     -d '{
       "Password": "NewSecurePassword123!"
     }' \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/users/00000000-0000-0000-0000-000000000000
```

3. **Delete or update default credential:**

```bash
curl -X DELETE \
     -H "Authorization: Bearer litegraphadmin" \
     http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000
```

### Token Management

- Use strong, randomly generated tokens (minimum 32 characters)
- Rotate tokens regularly
- Implement token expiration for bearer tokens
- Log token usage for audit purposes
- Never commit tokens to version control

### Network Security

- Always use HTTPS in production
- Implement rate limiting
- Use IP whitelisting where appropriate
- Deploy behind a reverse proxy
- Enable CORS only for trusted domains

### Password Policies

Implement strong password requirements:

- Minimum length: 12 characters
- Require mixed case letters
- Require numbers and special characters
- Prevent password reuse
- Implement account lockout after failed attempts

## Multi-Tenant Authentication

### Tenant Isolation

Each user belongs to one or more tenants. Authentication is scoped to a specific tenant:

```bash
# User must specify which tenant they're accessing
curl -H "x-email: user@example.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: tenant-guid-here" \
     http://localhost:8701/v1.0/tenants/tenant-guid-here/graphs
```

### Cross-Tenant Access

Users with access to multiple tenants must authenticate separately for each tenant:

1. List available tenants:

```bash
curl -H "x-email: user@example.com" \
     http://localhost:8701/v1.0/token/tenants
```

2. Generate token for specific tenant:

```bash
curl -H "x-email: user@example.com" \
     -H "x-password: password" \
     -H "x-tenant-guid: chosen-tenant-guid" \
     http://localhost:8701/v1.0/token
```

## Troubleshooting Authentication

### Common Issues

#### 401 Unauthorized

- Verify credentials are correct
- Check token hasn't expired
- Ensure tenant GUID is valid
- Confirm user is active

#### 403 Forbidden

- User lacks permission for the operation
- Attempting admin operation without admin token
- Accessing wrong tenant

#### Token Generation Fails

- Invalid email/password combination
- User account is inactive
- Tenant doesn't exist
- Tenant is inactive

### Debug Authentication

Enable authentication debugging in `litegraph.json`:

```json
{
  "Debug": {
    "Authentication": true
  }
}
```

Check logs for detailed authentication information:

```bash
tail -f ./logs/litegraph.log
```

## Integration Examples

### Python Example

```python
import requests
import json

# Using bearer token
headers = {
    'Authorization': 'Bearer default',
    'Content-Type': 'application/json'
}

response = requests.get(
    'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs',
    headers=headers
)

# Using security token
def get_security_token(email, password, tenant_guid):
    headers = {
        'x-email': email,
        'x-password': password,
        'x-tenant-guid': tenant_guid
    }

    response = requests.get(
        'http://localhost:8701/v1.0/token',
        headers=headers
    )

    return response.json()['Token']

token = get_security_token('default@user.com', 'password', '00000000-0000-0000-0000-000000000000')

headers = {
    'x-token': token,
    'Content-Type': 'application/json'
}

response = requests.get(
    'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs',
    headers=headers
)
```

### JavaScript Example

```javascript
// Using fetch with bearer token
const response = await fetch(
  "http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs",
  {
    headers: {
      Authorization: "Bearer default",
      "Content-Type": "application/json",
    },
  }
);

// Get security token
async function getSecurityToken(email, password, tenantGuid) {
  const response = await fetch("http://localhost:8701/v1.0/token", {
    headers: {
      "x-email": email,
      "x-password": password,
      "x-tenant-guid": tenantGuid,
    },
  });

  const data = await response.json();
  return data.Token;
}

const token = await getSecurityToken(
  "default@user.com",
  "password",
  "00000000-0000-0000-0000-000000000000"
);

const graphResponse = await fetch(
  "http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/graphs",
  {
    headers: {
      "x-token": token,
      "Content-Type": "application/json",
    },
  }
);
```

## Summary

LiteGraph provides flexible authentication options suitable for different use cases:

- **Admin tokens** for system administration
- **User credentials** for direct user authentication
- **Bearer tokens** for API integration
- **Security tokens** for session-based web applications

Choose the appropriate method based on your security requirements and use case. Always follow security best practices and change all default credentials before deploying to production.

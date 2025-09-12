---
title: Delete Credential
excerpt: >-
  Delete existing authentication credentials permanently, revoking access and
  removing bearer tokens with proper security validation.
deprecated: false
hidden: false
metadata:
  robots: index
---
## Overview

The Delete Credential endpoint allows you to permanently remove authentication credentials from a tenant. This functionality is essential for:

* Revoking compromised or expired credentials
* Removing unused or unnecessary authentication tokens
* Implementing credential lifecycle management
* Maintaining security by cleaning up old credentials
* Managing user access control and permissions

**Warning**: Credential deletion is irreversible. All access using the deleted credential will be immediately revoked.

**Important**: Credential deletion requires appropriate permissions within the tenant and must use a valid authentication token.

## Delete Credential

Remove an existing credential permanently using `DELETE: /v1.0/tenants/{tenant-guid}/credentials/{credential-guid}`. This endpoint permanently removes the credential and immediately revokes all access associated with it.

```curl
curl --location --request DELETE 'http://localhost:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000/credentials/00000000-0000-0000-0000-000000000000' \
--header 'content-type: application/json' \
--header 'Authorization: ••••••' \
--data ''
```
```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const deleteCredential = async () => {
  try {
    const data = await api.Credential.delete("<credential-guid>");
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

def delete_credential():
    litegraph.Credential.delete(guid="credential-guid")
    print("Credential deleted")

delete_credential()
```
```csharp
using LiteGraph;
using LiteGraph.GraphRepositories.Sqlite;

LiteGraphClient liteGraph = new LiteGraphClient(new SqliteGraphRepository("litegraph.db"));
liteGraph.InitializeRepository();
liteGraph.Credential.DeleteByGuid(Guid.Parse("<tenant-guid>"), Guid.Parse("<credential-guid>"));
```

## Response

Upon successful deletion, the API returns a `200 No Content` status code, indicating that the credential has been successfully removed. No response body is returned for successful deletions.

## Best Practices

When deleting credentials, consider the following security recommendations:

1. **Verify Credential Usage**: Check if the credential is actively being used before deletion
2. **Notify Users**: Inform users about credential revocation before deletion
3. **Confirm Deletion**: Double-check the credential GUID to ensure you're deleting the correct credential

## Next Steps

After successfully deleting a credential, you can:

* Update any systems that were using the deleted credential
* Create replacement credentials if needed
* Review remaining credentials in the tenant
* Implement credential lifecycle management policies
* Update credential management documentation
* Set up automated credential monitoring and cleanup
* Implement credential expiration and rotation workflows

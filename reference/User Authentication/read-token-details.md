---
title: Read Token Details
excerpt: Retrieve Authentication token deatils
deprecated: false
hidden: false
metadata:
  robots: index
---

To retrieve authentication token, call `GET /v1.0/token/details`

```curl
curl --location --request GET 'http://localhost:8701/v1.0/token/details' \
--header 'x-token: ******' \
--header 'Authorization: ••••••'
```

```javascript
import { LiteGraphSdk } from "litegraphdb";

var api = new LiteGraphSdk(
  "http://localhost:8701/",
  "<Tenant-Guid>",
  "*******"
);

const getTokenDetails = async () => {
  try {
    const token = "******";
    const data = await api.Authentication.getTokenDetails(token);
    console.log(data, "Token details retrieved successfully");
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
    access_key="*****",
)

def retrieve_token_details():
    token_details = litegraph.Authentication.retrieve_token_details(token="******")
    print(token_details)

retrieve_token_details()

```

### Response

```json
{
  "TimestampUtc": "2025-01-31T04:44:54.654309Z",
  "ExpirationUtc": "2025-02-01T04:44:54.654310Z",
  "IsExpired": false,
  "TenantGUID": "00000000-0000-0000-0000-000000000000",
  "Tenant": {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "Name": "Updated tenant",
    "Active": true,
    "CreatedUtc": "2025-08-29T13:54:54.956041Z",
    "LastUpdateUtc": "2025-09-08T10:00:45.175616Z"
  },
  "UserGUID": "00000000-0000-0000-0000-000000000000",
  "User": {
    "GUID": "00000000-0000-0000-0000-000000000000",
    "TenantGUID": "00000000-0000-0000-0000-000000000000",
    "FirstName": "Again Updated",
    "LastName": "User",
    "Email": "anotherbbb@user.com",
    "Active": true,
    "CreatedUtc": "2025-08-29T13:54:55.050579Z",
    "LastUpdateUtc": "2025-09-08T10:01:29.629367Z"
  },
  "Valid": true
}
```

<br />

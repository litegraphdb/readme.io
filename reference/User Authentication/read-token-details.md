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
import { LiteGraphSdk } from 'litegraphdb';

var api = new LiteGraphSdk('http://localhost:8701/', '<Tenant-Guid>', '*******');

const getTokenDetails = async () => {
  try {
    const token = '******';
    const data = await api.Authentication.getTokenDetails(token);
    console.log(data, 'Token details retrieved successfully');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
```python
import litegraph

sdk = litegraph.configure(
    endpoint="http://localhost:8701",
    tenant_guid="00000000-0000-0000-0000-000000000000",
    access_key="litegraphadmin",
)

def retrieve_token_details():
    token_details = litegraph.Authentication.retrieve_token_details(token="******")
    print(token_details)
    
retrieve_token_details()

```

<br />

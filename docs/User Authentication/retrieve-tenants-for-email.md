---
title: Retrieve tenants for email
excerpt: get tenants linked to particular email
deprecated: false
hidden: false
metadata:
  robots: index
---
To get tenants linked to particular email, call GET /v1.0/token/tenants

```curl
curl --location --request GET 'http://localhost:8701/v1.0/token/tenants' \
--header 'x-email: default@user.com' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
const getTenantsForEmail = async () => {
  try {
    const data = await api.Authentication.getTenantsForEmail('user@example.com');
    console.log(data, 'Tenants retrieved successfully');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```

<br />

---
title: Generate Auth Token
excerpt: Generate authentication token
deprecated: false
hidden: false
metadata:
  robots: index
---
To generate authentication token (using password), call GET /v1.0/token

```curl
curl --location --request GET 'http://localhost:8701/v1.0/token' \
--header 'x-email: default@user.com' \
--header 'x-password: password' \
--header 'x-tenant-guid: 00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript
```

<br />

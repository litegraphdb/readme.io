---
title: Exist
excerpt: To check if given tannat exist by id.
deprecated: false
hidden: false
metadata:
  robots: index
---
```curl
curl --location --head 'http://view.homedns.org:8701/v1.0/tenants/00000000-0000-0000-0000-000000000000' \
--header 'Authorization: Bearer litegraphadmin'
```
```javascript

const tenantExists = async () => {
  try {
    const data = await api.Tenant.exists('029b9092-3a4c-4f5e-8527-b1b947494e32');
    console.log(data, 'chk data');
  } catch (err) {
    console.log('err:', JSON.stringify(err));
  }
};
```
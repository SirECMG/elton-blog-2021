---
date: 2025-06-14
---

# publish static website to azure

the following doc will show you how to configure and deploy your static blog to azure. it assumes you already followed the directions in [link_to_azure_docs](https://learn.microsoft.com/en-us/azure/static-web-apps/publish-jekyll)

# build static site generator
```
mkdocs build
```

# save output path for azure
- after running `mkdocs build` it generates an output folder "site/".
- you need to modify .github/workflows/azure-static-web-apps-[YOUR_APP_NAME].yml

![image showing what to modify](./publish-static-site-azure/image.png)

# make custom domain changes in azure
Follow the steps in the two sections below to configure and sync both cloud provider and dns provider domain configs.

## Cloud Provider (Azure)
1. Go to "Custom domains" tab on the left under "Settings".
2. Click "+ Add" then "New Custom Domain on other DNS"
3. Enter "Domain name", i.e "www.eltonmurillo.com"
4. Select "Hostname record type", I chose "CNAME"
    - It can take up to 48 hours for DNS entry changes to take effect.

## DNS Provider
5. Go to your DNS provider
6. Under Advanced DNS in my case,  try to find "HOST RECORDS"
7. Go to "ADD NEW RECORD", then add
    - Type: CNAME Record
    - Host: www
    - Value: green-red-blah.2.azurestaticapps.net (should match the "Auto-generated" name from "Custom domains tab" in Cloud Provider)
    - TTL: Automatic

8. Done!


## reference doc
- [reference doc](https://learn.microsoft.com/en-us/azure/static-web-apps/publish-jekyll)

## update domain

- [internal domain](https://learn.microsoft.com/en-us/azure/static-web-apps/custom-domain)
- [external domain](https://learn.microsoft.com/en-us/azure/static-web-apps/custom-domain-external)

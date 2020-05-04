---
published: false
---

## Hosting Angular/Ionic Apps For (Almost) FREE

### Create App
Create an app using your favorite framework and compile it for production. I use Azure Devops to release to my Azure Storage site. I will detail that in another post. 

### Host a static website in Azure Storage
https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to?tabs=azure-portal

### Integrate a static website with Azure CDN
https://docs.microsoft.com/en-us/azure/storage/blobs/static-website-content-delivery-network
- This is needed for the custom domain name
- Azure CDN also gives you a certificate and SSL configuration which is a huge plus!

### Custom Domain Name
https://docs.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal
- In my DNS Settings on GoDaddy, I adjust the www CNAME entry to point to my yoursitename.azureeduge.net.


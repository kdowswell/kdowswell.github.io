---
published: false
---

## Hosting Javascript Apps For (Almost) FREE
Hosting an app can be expensive if you don't do it correctly. A lot of articles talk about pushing your client side apps to App Services or other options that are not cost effective. Azure Storage is the cheapest, fastest, and best option for most. 

Pairing this up with an Azure Functions based API and you can reduce costs from potentially $100+ to Dollars 
Azure Functions would need to be called 10,000,000 times to cost $1.80 for the month.

### Costs
**Azure App Services**
with SSL and Custom Domain name will run you somewhere around $54 based on their current calculations.

**Azure Storage Account**
According to the Azure calcualtions tool this will cost $0.06 a month. This also gets you global CDN distribution in addition to SSL and Custom Domain name support. It requires a few more steps but cost savings for static client apps or sites are a no-brainer.

### Create App
Create an app using your favorite framework and compile it for production. I use Azure Devops to release to my Azure Storage site. I will detail that in another post. 

### Host a static website in Azure Storage
[Microsoft Tutorial - static website in Azure Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website-how-to?tabs=azure-portal)

### Integrate a static website with Azure CDN
[Microsoft Tutorial - static website with Azure CDN](https://docs.microsoft.com/en-us/azure/storage/blobs/static-website-content-delivery-network)
- This is needed for the custom domain name
- Azure CDN also gives you a certificate and SSL configuration which is a huge plus!

### Custom Domain Name
[Microsoft Tutorial - Custom Domain Name](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-custom-domain-name?tabs=azure-portal)
- In my DNS Settings on GoDaddy, I adjust the www CNAME entry to point to my yoursitename.azureeduge.net.

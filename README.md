# Overview
The examples provided in this project are meant to illustrate how to utilize the TRACT 
Hosted Payment IFrame browser based payment capture to meet your business needs.

This example required an initial authenticated call to TRACT via a secure mechanism to retrieve a 
referrer token.

# Prerequisites 
* node.js is installed on your environment

    * See https://nodejs.org/en/download/
    * Tested with node version 8.6.0 

* Navigate to root /payments.js folder and do the following

    * npm install
    * This will install all the requirements required to run the samples.

* A TRACT tenant

    * goTransverse Customer Support will provide the domain name for your TRACT instance, (e.g. demo.tractbilling.com for the purposes of these examples)
    * goTransverse Customer Support will provide an api account for you TRACT tenant.
    * A customer defined and managed origin domain that will host the page
        * goTransverse Customer Support will need to configure a hosted payment page endpoint with this origin domain
        * This is required so that an X-Frame-Options header can be properly enabled for this origin domain
        * A single origin domain can be used for multiple tenants within a single TRACT environment, however a different domain is required per environment (eg. dev.my-domain.com
        versus stage.my-domain.com versus prod.my-domain.com)
    
    
# Getting A Referrer Token

Using a tool like Postman, construct an HTTP post with the following information

```https://demo.tractbilling.com/t/s/r/1.33/payments/referrerToken```


## Request Headers

```Authorization: Basic <auth>``` 

```Content-Type: application/xml```
    
   Where `<auth>` is the base64 encoded <your-username>:<your-password>

    
## Request Body
```
<?xml version="1.0" encoding="UTF-8"?>
<generatePaymentCollectionReferrerToken xmlns="http://www.tractbilling.com/billing/1_33/domain">
    <errorUrl>http://localhost:1111/error.html</errorUrl>
    <cancelUrl>http://localhost:1111/cancel.html</cancelUrl>
    <completeUrl>http://localhost:1111/success.html</completeUrl>
</generatePaymentCollectionReferrerToken>        
```

## Response Body
```        
<?xml version="1.0" encoding="UTF-8"?>
<referrer xmlns="http://www.tractbilling.com/billing/1_33/domain" referrerToken="d88f9360-e192-412e-8892-9f5adb24e844"/> 
```
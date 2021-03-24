# Email Address

Email address API method can create, update, and delete email address of an existing customer. Fetch a specific email address or all email addresses of a customer.


### Endpoints
See all [Email address API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5ddde1a62bd5ea6d280dfe70?&tags=EmailAddresses).



| POSTYellow Email Address | /customers/{customerId}/emailAddresses | 
|  --- |  --- | 
| GETGreen Email Address | /customers/{customerId}/emailAddresses/{emailAddressId} | 
| GETGreen  Email Addresses | /customers/{customerId}/emailAddresses | 
| PUTBlue Email Address | /customers/{customerId}/emailAddresses/{emailAddressId} | 
| DELETERed Email Address | /customers/{customerId}/emailAddresses/{emailAddressId} | 


## Workflow

### Add a new email address workflow
01014155122281255670914create-email111https://debitsuccess.atlassian.net/wikicreate-email0971383
### Update an email address workflow
01012719562981255670914upadte-email.drawio111https://debitsuccess.atlassian.net/wikiupadte-email.drawio01187383

 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Email Address Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| EmailAddressId | string(10) | Unique identifier associated with the Contact. | 
| EmailName | string(50) | Name of person to be contacted | 
| EmailAddress | string(75) | The actual email address. Example,[myemailaddress@domain.com](mailto:myemailaddress@domain.com) | 
| IsPrimary | 'false' / 'true' | Flag for indication of preferred email address. If a customer has multiple emails, only 1 can be marked as preferred. | 


### Sample Email Address

```json
{
   "emailAddressId":"7777777",
   "name":"john",
   "emailAddress":"john.doe@debitsuccess.com",
   "isPrimary":"false"
}
```


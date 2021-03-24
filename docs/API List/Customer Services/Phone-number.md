Phone Number API method can create, update, and delete an email address of an existing customer. Fetch a specific phone number or all phone numbers of a customer. 


### Endpoints
See all [Phone Number API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5ddde18fb48942b2d52c7a8e?&tags=PhoneNumbers).



| POSTYellow Phone Number | /customers/{customerId}/phoneNumbers | 
|  --- |  --- | 
| GETGreen Phone Number | /customers/{customerId}/phoneNumbers/{phoneNumberId} | 
| GETGreen  Phone Numbers | /customers/{customerId}/phoneNumbers | 
| PUTBlue Phone Number | /customers/{customerId}/phoneNumbers/{phoneNumberId} | 
| DELETERed Phone Number | /customers/{customerId}/phoneNumbers/{phoneNumberId} | 


## Workflow

### Create new phone number workflow
01015877081781255670914createphonenumberflow.drawio111https://debitsuccess.atlassian.net/wikicreatephonenumberflow.drawio0971383
### Update a phone number workflow
01015871517961255670914Updatephonenumber.drawio111https://debitsuccess.atlassian.net/wikiUpdatephonenumber.drawio01187.0000000000005383.0000000000001

 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Phone Number Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| PhoneNumberId | string(10) | Unique identifier associated with the Contact. | 
| PhoneType | Enum - Emergency, Fax, Home, Mobile, Work | Contact Type | 
| PhoneName | string(50) | Name of person to be contacted | 
| IsPrimary | 'false' / 'true' | Flag for indication of preferred contact.if a customer has multiple contact types, only 1 can be marked as preferred. | 
| PhoneNumber | string(75) | Details of contact.e.g. Phone number or email | 
| AreaCode | string(4) | Area code of a phone number. E.g. 02, 07 | 
| CountryCode | string(4) | Country code of a phone number. E.g. +61, +64 | 


### Sample Phone Number Object

```
{
   "phoneNumberId":"7777777",
   "name":"john",
   "countryCode":"+64",
   "areaCode":"09",
   "type":"mobile",
   "phoneNumber":"264 5555",
   "isPrimary":"true"
}
```






*****

[[category.storage-team]] 
[[category.confluence]] 

# Address

Address API method can create, update, and delete address of an existing customer. Fetch a specific address or all addresses of a customer. 


### Endpoints
See all [Address API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5ddddcd07f477580b89057cd?&tags=Addresses).



| POSTYellow Address | /customers/{customerId}/addresses | 
|  --- |  --- | 
| GETGreen Address | /customers/{customerId}/addresses/{addressId} | 
| GETGreen  Addresses | /customers/{customerId}/addresses | 
| PUTBlue Address | /customers/{customerId}/addresses/{addressId} | 
| DELETERed Address | /customers/{customerId}/addresses/{addressId} | 


## Workflows

### Create a new address workflow
01012620309191255670914add-address.drawio144https://debitsuccess.atlassian.net/wikiadd-address.drawio0971383
### Update an Address workflow
01014155450511255670914update-address122https://debitsuccess.atlassian.net/wikiupdate-address01187383

 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Address Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| AddressId | string(10) | Unique identifier associated with the Address.NOTE: this is useful when PUT Addresses API requires an input parameter to uniquely identified the exact address to be updated. | 
| AddressLine1 | string(60) | Address line | 
| AddressLine2 | string(60) | Address line 2 is used when the total address length exceeded Address1, i.e. longer than 60 characters. | 
| Suburb | string(50) | Suburb | 
| City | string(50) | City | 
| Postcode | string(10) | Postcode | 
| State | string(3) | 2 or 3 letters code representing the state. Refer to[State Codes](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1257414195/Reference#StateCode-(USA-and-AUS))for sample state codes for US and Australia. This field also used to captured Provinces if applicable | 
| CountryISOCode | string(4) | Country ISO code. Refer to[CountryISOCode](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1257414195/Reference#CountryISOCode). | 
| AddressType | Enum -  | Address Type.  Note: Customers are not allowed to have multiple addresses with same Address Type | 
| IsPrimary | 'false' / 'true' | Flag to indicate if an address type is preferred for mailing | 


### Sample Address Object

```json
{
   "addressId":"8888888",
   "addressLine1":"5 The warehouse way",
   "addressLine2":"Northcote",
   "suburb":"Northcote",
   "state":"",
   "city":"Auckland",
   "postcode":"1062",
   "countryISOCode":"NZ",
   "type":"Home",
   "isPrimary":"false"
}
```


*****

[[category.storage-team]] 
[[category.confluence]] 

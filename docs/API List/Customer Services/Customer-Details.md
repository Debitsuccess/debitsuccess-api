#Customer

A customer is anyone who is a members of health and fitness companies, policyholders of insurance, parents of children who attend child care centres. Debitsuccess collects payments from them for the services offered by the businesses. Customer API methods enable the business to execute customer information related to functionalities. Customer API can create, delete, and update personal and contact detail information of a customer. Fetch specific customer information and list all customers’ details. 


### Endpoints
See all [customer APIs](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/customers?tags=Customers&pattern=&groupBy=).



| POSTYellow Customer | /customers | 
|  --- |  --- | 
| GETGreen Customer | /customers/{customerId} | 
| GETGreen  Customers | /customers | 
| PUTBlue Customer | /customers/{customerId} | 


## Workflows

### Create Customer workflow
01012701211251255670914create-customer.drawio155https://debitsuccess.atlassian.net/wikicreate-customer.drawio0undefined950383
### Update customer details workflow
01012700558281255670914update-customer.drawio122https://debitsuccess.atlassian.net/wikiupdate-customer.drawio0897383 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Customer Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| CustomerId | string(10) | Unique identifier associated with the Customer. | 
| Business<ul><li>BusinessId

</li><li>Name

</li></ul> | <ul><li>string(10)

</li><li>string(50)

</li></ul> | <ul><li>Unique identifier associated with the Facility

</li><li>Name associated with the Facility

</li></ul> | 
| CustomerType | Enum ( Individual, Business) | Indicate the type of customer, i.e. Individual or Business | 
| Title | string(10) | Title used to address the Customer. E.g. Mr, Dr, Ms | 
| FirstName | string(40) | Given name/first name associated with the Customer. | 
| MiddleName | string(40) | Middle name associated with the Customer. | 
| LastName | string(40) | Family name/last name associated with the Customer. | 
| Gender | string | Customer gender. | 
| DateOfBirth | 'YYYY-MM-DD' | Customer date of birth. Must not be future date. | 


### Sample Customer Object

```json
{
   "customerId":"1234567",
   "business":{
      "businessId":"3333333",
      "name":"Debitsuccess 24/7 Fitness"
    },
   "customerType":"Individual",
   "title":"Mr",
   "firstName":"John",
   "middleName":"smith",
   "lastName":"doe",
   "gender":"Male",
   "dateOfBirth":"2019-01-01"  
}
```




## Accounts
Account referred to the contract of our client with their customers for the services offered by the client. Within the Account API, you can execute account management functions through the API methods, including:


* Get information about an account, overdue status and account.


* Create an account with a payment schedule.


* Adjust the contract amountand change the terms of an account.


* Update default payment method for an existing account


* Get a list all accounts within a business based on various search criteria.




### Endpoints
See all [account APIs](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5dc1d4af15ad1d4dea48b781?tags=Accounts&pattern=&groupBy=tag).



| POSTYellow Account | /accounts | 
|  --- |  --- | 
| POSTYellow  Cancel Account | /accounts/{accountId}/cancellation | 
| GETGreen Account | /accounts/{accountId} | 
| GETGreen Accounts | /accounts | 
| PUTBlue Account | /accounts/{accountId} | 
| PATCH Account | /accounts/{accountId} | 


## Workflows

### Create billing account workflow
10098513718112574733181Createbillingaccount.drawio88https://debitsuccess.atlassian.net/wikiUntitled Diagram.drawio0undefined1230383
### Create a new account for an existing customer
10098513718115877410651accountforexistingcustomer22https://debitsuccess.atlassian.net/wikiaccountforexistingcustomer01170.5383
### Update existing account
10098513718115876755221updateAcc.drawio11https://debitsuccess.atlassian.net/wikiupdateAcc.drawio01173.0000000000002382.9999999999999
### Cancel account
10098513718115870535001Cancelaccount.drawio11https://debitsuccess.atlassian.net/wikiCancelaccount.drawio01170.4999999999998383.0000000000001 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Account Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| CustomerId | string/integer | Unique identifier associated with the Customer.Required to identify the customer whom this account will be created for. | 
| BusinessAccountId | string(6) | Provided by Debitsuccess to identify a Facility Account.Required to identify the facility account where the newly created account will be associated. Accepted values: a-z, A-Z, 0-9, -, _ | 
| AccountExternalId | string(50) | External reference number associated to the Accountto be created | 
| AccountCode | string(100) | Account code associated to the Accountto be created | 
| TermType | months / payments | Term type, e.g. Payments or MonthsM - Months,P - Payments | 
| Term | integer | Number of terms to complete the recurring payments | 
| AccountNotes | text,1000 | Free form notes field | 
| FixedTerm | false / true | true - account will be closed at the end of the minimum termfalse - account will continue to bill after minimum term | 
| WaiveEstFee | false / truedefault to false | A flag to waive establishment fee, defaulted to be paid by Customer. | 
| AccountStartDate | 'YYYY-MM-DD' | Specify the desired start date (in UTC) when the account should start. Must not be a date in the past. | 
| ContractAmount | numeric(10,2) | Amount to be collected for the account (in terms of recurring payments) before the account is past its minimum term.Applicable for fixedTerm = true | 
| PaymentMethodToken | Token | PaymentMethod must be associated to the providedCustomerId | 
| RecurringSchedules()<ul><li>RecurringScheduleStartDate \*\*

</li></ul> | 'YYYY-MM-DD' | Recurring Schedule start date. | 
| <ul><li>Installment

</li></ul> | numberic(8,2) | Amount to pay for each installment.Must be greater than or equal to $1 | 
| <ul><li>Frequency

</li></ul> | Enum: \[weekly, fortnightly, four-weekly, monthly, bi-monthly, quarterly] | Frequency of the recurring schedule | 
| <ul><li>NumberOfPayments

</li></ul> | integer | Total payments required for the schedules. Not required for account's last schedule | 
| <ul><li>ExternalScheduleId

</li></ul> | string(50) | External identifier of the recurring schedule | 
| <ul><li>ScheduleDescription

</li></ul> | string(50) | Used to capture the description of the schedule | 


### Sample Account Object

```json
{
   "customerId":"1234567",
   "businessAccountId":"DSFit1",
   "accountExternalId":"100200300ABCD",
   "accountCode":"AC1234567890",
   "termType":"months",
   "term":12,
   "accountNotes":"This is dedicated to account notes. Max allowed 1000 characters.",
   "fixedTerm":true,
   "waiveEstFee":true,
   "accountStartDate":"2019-12-31",
   "contractAmount":900.00,
   "recurringSchedules":[
      {
         "recurringScheduleStartDate":"2020-01-31",
         "installment":50.00,
         "frequency":"monthly",
         "numberOfPayments":6,
         "externalScheduleId":"R125810",
         "scheduleDescription":"Recurring schedule Jan-Jun"
      },
      {
         "recurringScheduleStartDate":"2020-07-31",
         "installment":100.00,
         "frequency":"monthly",
         "numberOfPayments":null,
         "externalScheduleId":"R125811",
         "scheduleDescription":"Recurring schedule Jul-Dec"
      }
   ]
}
```












*****

[[category.storage-team]] 
[[category.confluence]] 

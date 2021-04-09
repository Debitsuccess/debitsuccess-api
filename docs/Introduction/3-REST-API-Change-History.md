# Change Log


##  Mar 23, 2021
The RestAPI [GET Account(s)](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5dc1d4af15ad1d4dea48b781?&tags=Accounts) is enhanced to return the DD Stop reason field in the API Response. If the account status ‘PaymentStopped’ is set to true and has a CollectionStopReason assigned, then it will be shown in the GET Account(s) API response CollectionStopReason field, else an empty string will be returned.

## Mar 16, 2010

Introduced a new field Active as an input parameter for [GET BusinessAccounts](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5da67acb981fb494d4d20b42?&tags=BusinessAccounts). This field will act as a filter to allow users to retrieve Active or non-Active Business Accounts. Leaving this field as Null/empty will retrieve all Business Accounts.

## Feb 23, 2021
Implemented a new REST API[Get Payment Token(for Casual Payment)](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/6032d38d4c55a6c59ff9de42?&groupBy=tag) that generates and returns a PayNow URL link so that integrators can access the link to make a casual payment for a business account.


## Feb 11, 2021
A new REST API [Get PaymentToken (for Account Payment)](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/60231eec62d17ed94b9acda8?&groupBy=tag) has been implemented to generate and return a PayNow URL link so that integrators can access the link to make payment to an account.


## Jan 26, 2021

* The [GET Account(s)](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5dc1d4af15ad1d4dea48b781?tags=Accounts&pattern=&groupBy=tag) response message now includes AccountNotes and PaymentMethodToken to be consistent with the POST Account API response.


* The [POST Account](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5dc0a46f2f4e8967ea68c2ae?) response message has been updated with additional 23 fields similar to response for GET Account.



## Oct 29, 2020

All [Debitsuccess REST APIs](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1157791982/API+Resources) are now available in the production environment. Please contact us to obtain your credentials before using it on production. 

## Oct 22, 2020

Customer REST API is now available in the production environment. [Customer API](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1255670914/Customer+Details#Customer) allows the integrator to create, delete, and update the personal and contact detail information of a customer. Fetch specific customer information and list all customers’ details. 

******

## Upcoming APIs and Features
Debitsuccess is always improving how we deliver our service.As part of delivering updated features, we may make some changes that impact how some of our existing APIs return data.

Please note that these features are in is in our roadmap but we do not have a definite ETA.


* A new Realtime Payment Widget will be available soon to which allows you to securely make real-time payments to businesses. Integration partners can embed this widget into their website and customize it to match their product theme.


*****


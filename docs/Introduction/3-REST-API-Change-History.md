# Change Log

All notable changes to Debitsuccess REST APIs are documented below.

*****
## Sept 6, 2022
Implemented a new endpoint i.e., [GET Surcharge Configurations](https://debitsuccess.stoplight.io/docs/debitsuccess-api/a35250ea5005c-get-surcharge-configurations) which returns surcharge percentage and amount for a facility account.

## Sept 21, 2021
GET [Business Account(s)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODE-list-business-accounts) response message now includes `Commission fee` details for each payment type configured for the business account.

## Sept 2, 2021
GET [PaymentHistory](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MTk-get-payment-history) is enhanced to return commission amount in the response. 

## Jul 13, 2021
This release introduces a new boolean field named `assignExistingGuarantor` in [POST Account](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODM-create-account) to allow users to assign an existing Guarantor to the new account when the account is created.

## Jul 08, 2021
Introduced new endpoints:
* [PUT Guarantor](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MzA-update-guarantor) - allows users to update Guarantor details for existing active accounts
* [GET Guarantor](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MzE-get-guarantor) - allows users to get Guarantor details for existing active accounts

## Jul 06, 2021
Implemented a new endpoint i.e., [POST Guarantor](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5Mjk-create-guarantor) which allows users to create Guarantor record for existing active accounts.

## Jun 17, 2021
* Introduced a new endpoint for customer services API will be used to [transfer an account](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5Mjg-transfer-account) from one business account to another.

* Enhanced the existing REST API endpoint [PUT Account](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODY-update-account):

  * The `collectionStopReason` in [GET Account(s)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODQ-list-accounts) response defaults to *Manual Payment Stop* when `paymentStopped` is set to *true* in PUT Account.

  * New Error 400 introduced to reject PUT Account request if `collectionStopReason` is not *Manual Payment Stop*.


## May 25, 2021
Enhancement to populate standardized 403 error messages when client attempts to execute API request with the resources provided in the request URL that has not been authorized to them. There are four types of resources i.e., account, customer, business, and business account where each type will return error code 403 with standard errors message depending on the resource type.

## May 20, 2021 

* Introduced a new endpoint for customer services API that will retrieve customer [payment schedule statuses](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5Mjc-get-payment-status) and other details for Gateway Model accounts.
* Implemented multilevel permission checks for [GET Payment History](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MTk-get-payment-history) endpoints by filter off all records that the client do not have access to.
* Fix to stop 'Overdue' mail if Account has a new schedule created (via POST Account/POST Schedule) to start immediately but after the billing cycle for the day has completed. This is to prevent sending an overdue email to the customer.

## May 11, 2021

The [Real Time Payment Widget](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Widgets/Real-time-payment-widget.md) allows you to securely make real-time payments to businesses (Casual Payments). Integration partners can embed this widget into their website and customize it to match their product theme. Widget is essentially an iframe to capture credit card details and use Debitsuccess [Payments API](https://debitsuccess.stoplight.io/docs/debitsuccess-api/PaymentsAPI.v1.json) to make payments. 

##  Mar 23, 2021
The RestAPI [GET Account(s)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODQ-list-accounts) is enhanced to return the DD Stop reason field in the API Response. If the account status ‘PaymentStopped’ is set to true and has a `CollectionStopReason` assigned, then it will be shown in the GET Account(s) API response CollectionStopReason field, else an empty string will be returned.

## Mar 16, 2010

Introduced a new field `Active` as an input parameter for [GET BusinessAccounts](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODE-list-business-accounts). This field will act as a filter to allow users to retrieve Active or non-Active Business Accounts. Leaving this field as null/empty will retrieve all Business Accounts.

## Feb 23, 2021
Implemented a new REST API[Get Payment Token(for Casual Payment)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MjY-generate-payment-token-for-casual-payment) that generates and returns a PayNow URL link so that integrators can access the link to make a casual payment for a business account.


## Feb 11, 2021
A new REST API [Get PaymentToken (for Account Payment)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM5MjU-generate-payment-token-for-account-payment) has been implemented to generate and return a PayNow URL link so that integrators can access the link to make payment to an account.


## Jan 26, 2021

* The [GET Account(s)](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODQ-list-accounts) response message now includes AccountNotes and PaymentMethodToken to be consistent with the POST Account API response.


* The [POST Account](https://debitsuccess.stoplight.io/docs/debitsuccess-api/b3A6MTc2MTM4ODM-create-account) response message has been updated with additional 23 fields similar to response for GET Account.



## Oct 29, 2020

All [Debitsuccess REST APIs](../Introduction/1-REST-APIs.md) are now available in the production environment. Please contact us to obtain your live environment credentials before using them on production. 

## Oct 22, 2020

Customer Services REST API is now available in the production environment. [Customer API](https://debitsuccess.stoplight.io/docs/debitsuccess-api/YXBpOjE3NjEzNzQ4-customer-services-api) allows the integrator to create, delete, and update the personal and contact detail information of a customer. Fetch specific customer information and list all customers’ details. 

******




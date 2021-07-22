# Glossary 

## A

### accountCloseDate
The date when the account was closed.


### accountCode
Account code from contract


### accountExternalId
Unique reference/ identifier for the account provided by the business. This will be recorded for reference but it cannot be used for other operations. Businesses will have to query and use accountId for operations. The accountExternalId must be unique per Business Account.


### accountId
Unique reference/ identifier for the account provided by Debitsuccess. Business can use this parameter for other operations on the account.


### accountLoadedDatetime
The date and time when the account was loaded. It will be in UTC format


### accountNotes
Free form notes field that can be used to capture account's activities and other account details


### accountStartDate
The date from which the account will be active.


### accountStatus
It can be used to filter retrieved account based on their current status. The default value is Active if not provided.  'Active' accounts can also be 'Suspended' or 'PaymentStopped' at the same time.  

'Suspended' accounts can also be 'PaymentStopped' at the same time. Descriptions of the status can be found [here](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1492877598/Statuses#Account-Status).


### accruedContractAmount
Amount to be collected for the account (in terms of recurring payments) before the account is past its minimum term.


### addressId
Unique reference/ identifier for the address provided by Debitsuccess. Business can use this parameter for other operations on the address.


### addressLine1
Street address 1  (e.g., street, PO Box, or company name).


### addressLine2
Street address 2 (e.g., apartment, suite, unit, or building).


### addressType
Type of the address provided such as Business, Home, Physical, or Postal.


### amount
Amount paid or due to be paid by the customer


### areaCode
The local area code for the phone number. It is applicable for landline numbers.


## B

### batchNumber
The batch number of a transaction that was processed


### businessAccountId
Unique reference/identifier provided by Debitsuccess which allows customer accounts to be split into different organizational groups or services if required.


### businessId
Unique reference/identifier provided by Debitsuccess for the business


### business.name
The trading name of the business


### businessAccount.name 
Business account name


## C

### cancellationNotes
Information provided by the business regarding the cancellation of the account


### cancelReason
The reason for the cancellation of the account. It could have been cancelled by the business or by Debitsuccess


### cardExpiryDate
Expiry date of the credit card


### cardType
The type of card that can be chosen depends on what card type is configured for the business. If you would like to enable/disable a particular type of card, kindly contact the Account Manager


### catchUpAmount
The amount arranged with the customer to catch up on overdue payments


### catchUpEndDate
End date for the catch-up arrangement with the customer


### city
City, district, town, or village.


### contractAmount
The total value of the contract signed by the customer.


### countryCode
The [country code](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#countrycode) associated with the phone number.


### countryISOCode
The three-character [ISO code](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#countryisocode) of the country.


### customerId
Unique reference/ identifier for the customer provided by Debitsuccess. Business can use this parameter for other operations on the customer.


### customerType
The type of customer record. There are only two options: Individual or Business. Capturing further information regarding the customer depends on the type of customer.


## D

### dateOfBirth
Date of birth of the customer


### datetimeOfPayment
Date time when a payment is collected. The time must be provided in UTC format.


### datetimeOfReversal
Date time when a payment is reversed/deleted. The time must be provided in UTC format.


### dateType
Type of date referred by fromDatetime and toDatetime to be used for filter


### defaultPaymentMethod
To indicate if a payment method must be marked as the primary payment method for an account. There can only be one payment method per account marked as default at a time.


### deleteFutureSchedule
Field to accept/acknowledge that future recurring schedules will be deleted when a new recurring schedule is attempted to be added ahead of it.


### description
For POST Business Collected Payment: the description of the payment.

For POST Reverse Business Collected Payment: the description of the reversed payment


### dueDate
The date when the schedule is due to be billed


## E

### emailAddress
Email address of the customer is being recorded


### emailAddressId
Unique reference/ identifier for the emailAddress provided by Debitsuccess. Business can use this parameter for other operations on the emailAddress.


### emailName
Name of the person whose email ID is being recorded


### externalPaymentIdentifier
Unique reference/ identifier for the payment send through by the business. This will be recorded for reference but it cannot be used for other operations.


### externalScheduleId
Unique reference/ identifier for the schedule provided by the business. This will be recorded for reference but it cannot be used for other operations. The business will have to query and use scheduleId for operations. The value has to be unique per business account.


## F

### firstName
The customer’s first name.


### fixedTerm
Field to be used when an account must be set to close. It will close when either the signed contract period ends and/or the contract amount has been collected.


### frequency
Payment frequency of a recurring instalment. It must be chosen from a pre-defined list.


### fromDatetime
Date range filter in UTC.


### fromOverdueAmount
Previous overdue amount.


### fromOverdueStatus
Previous overdue status value.


### fromOverdueStatusChangeDatetime
Datetime of previous overdue status change in UTC.


## G

### gender
The customer’s gender. 


## H

### hasNext
Indicates the existence of more rows. If the value is true, there are more rows.


### holderName
Name of the account holder when bank account details are provided. Name of the cardholder when credit card details are provided.


## I

### IncludeFees
Flag to indicate if Debitsuccess fee transactions should be extracted. Default to false if not provided.


### installment
Amount that will be collected on a recurring basis at a frequency provided by the business.


### isPrimary
To indicate whether a particular value must be considered the primary details. All the previous values will be maintained but set to non-primary.


## L

### lastBillingDatetime
Last datetime the account was billed on


### lastName
The customer’s first name.


### lastReversalReason
Reason for last payment failure


### lastUpdatedDatetime
Datetime when the account or a related record was last updated


### limit
Indicate the number of records to be fetched into the list. Default to a maximum value of 50 if not provided or value provided is greater than 50.


## M

### middleName
The customer’s middle name.


### minimumEffectiveDate
The date after which (on the next payment cycle) that the schedule will start


## N

### nextBillingDate
The next date the account is due to be billed on


### nextCursor
Indicates the position of the next record to be fetched into the list. Default to retrieve from the first record, if not provided.


### number
Field to provide the bank account number or credit card number


### numberOfPayments
The number of payment cycles to either bill the account or suspend the account. It is directly related to the frequency of the schedule.


## O

### order
Order in which the details must be retrieved


### originalContractAmount
The total value of the contract signed by the customer.


### originalId
Unique reference/ identifier for the payment collected by the business. It is provided by the business when the payment details are sent through. Business can use this parameter to reverse the original payment.


### outstandingFeeAmount
Amount remaining to pay in Debitsuccess Fees


### outstandingOneOffAmount
Amount remaining to pay in one-off charges (business charges)


### outstandingRecurringAmount
Amount remaining to pay in recurring installments (business charges)


### overdueAmountFee
Overdue amount to pay in Debitsuccess Fees


### overdueAmountPayment
Overdue amount to pay in business charges


### overdueStatus
0, 1, 2, 3 (0 = Not overdue, > 0 indicate overdue stages with increasing severity ). Status descriptions can be found in [Statuses in Debitsuccess Systems](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1492877598/Statuses+in+Debitsuccess+Systems#Account-Overdue-Status).


### overrideBillingCycleAlignment
true = Overrides default behaviour and sets the start date of the new payment schedule to be the minimum effective date. PreviousScheduleEndDate is required with this option.


## P

### paymentAmount
Amount paid


### paymentCode
[Transaction type](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#paymentcode)


### paymentDatetime
Date time when the payment was made


### paymentDescription
Description of payment


### paymentErrorCode
Payment [transaction error](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#paymenterrorcode), if any


### paymentId
Unique reference/ identifier for the payment provided by Debitsuccess. Business cannot use this parameter for other operations.


### paymentInAdvanceAmount
Amount paid in advance


### paymentInAdvanceEnddate
End date for payment in advance


### paymentMethod
[Mode of payment](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#paymentmethod)


### paymentMethodToken
The token generated by the payment method capture API to use as a reference for a particular payment method


### paymentMethodType
The type of payment method to be created.


### paymentStopEndDate
Date after which collection of charges/fees can resume.


### paymentStopped
A flag to indicate whether the account currently has a stop on collection.


### phoneName
Name of the person whose phone number is being recorded.


### phoneNumber
Phone Number to contact the customer


### phoneNumberId
Unique reference/ identifier for the phone number provided by Debitsuccess. Business can use this parameter for other operations on the phone Number.


### phoneType
Type of the phone number provided. 


### postcode
ZIP or postal code.


### previousScheduleEndDate
End date of the previous recurring schedule. It is recommended that you maintain the frequency of the previous schedule so that the account does not incur pro-rata payments


### projectedFinishDate
Calculated estimated time for the account finish date. This field is being calculated overnight.


## R

### recurringScheduleEndDate
Date when a recurring schedule ends.


### recurringScheduleStartDate
Date when a recurring schedule starts.


### retryCount
The number of retries accumulated for the payment.


### reversedPaymentId
Unique identifier for the reversed payment.


## S

### scheduleDescription
Description of the schedule


### scheduleId
Unique reference/ identifier for the schedule provided by Debitsuccess. Business can use this parameter for other operations on the schedule.


### state
[State code](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/6-Reference.md#statecode-usa-and-aus) for US and Australia.


### suburb
Part of the city or large town outside its centre.


### suspended
When set to true, the collection is suspended. The amount owing will NOT continue to accrue while collections are suspended.


### suspensionFee
Amount to charge for the suspension


### suspensionScheduleEndDate
The date on which the suspension shall end.


### suspensionScheduleStartDate
The date on which the suspension shall start.


## T

### term
Length of term.


### termsAndConditions.description
Description associated with the terms and conditions, if it is enabled


### termsHTML
HTML fragment with the terms and conditions of the business account, if it is enabled


### termsAndCondition.name
Name associated with the terms and conditions, if it is enabled


### termType
Months, Payments


### title
Title for the customer


### toDatetime
Date range filter in UTC


### toOverdueAmount
New overdue amount


### toOverdueStatus
A new overdue status value


### toOverdueStatusChangeDatetime
Datetime of overdue status change in UTC.


## W

### waiveEstFee
Can be used to override the establishment fee payer in case it is set to business by default and should be waived so that the business pays the establishment fee.



*****


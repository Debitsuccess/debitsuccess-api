# Businesses

Retrieves a list of business(es) (also known as Facility) assigned to the client ID that is used for authenticating with the Debitsuccess authentication server. Multiple businesses can be assigned to a single client ID.


### Endpoints
See all [Businesses API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/organisation?&tags=Businesses&groupBy=tag).



| GETGreen Businesses | /businesses/{businessId} | 
|  --- |  --- | 
| GETGreen Businesses | /businesses | 

 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Businesses Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| BusinessAccountId | string(6) | Contract prefix codeProvided by Debitsuccess to identify a Facility Account | 
| Name | string(50) | Name of Facility Account | 
| CommissionFee |  |  | 
| 
```
SupportedPaymentMethods
```
<ul><li>PaymentMethodType

</li></ul> | <ul><li>string(2)

</li></ul> | NOTES: Beside all supported CC, Payment Method type "Bank Account " should be included in the list. | 
| PenaltyFee<ul><li>Amount

</li><li>Payer

</li></ul> | <ul><li>number

</li><li>string

</li></ul> |     if PenaltyFeePayer = 0Payer = "Customer pays" ifPenaltyFeePayer = 1Payer = "Facility pays"     if PenaltyFeePayer= 2Payer = "No Fee" | 
| EstablishmentFee<ul><li>Amount

</li><li>Percent

</li><li>Payer

</li></ul> | <ul><li>number

</li><li>number

</li><li>string

</li></ul> | ifEstFee = 0 then Payer = "Facility Default",else if 1 = then payer = "Customer Pays" ,else if 2 = then payer = "Facility Pays",else if 3 = then payer "No Fee" | 
| Business<ul><li>BusinessId

</li><li>Name

</li></ul> | \[Business]<ul><li>string/integer

</li><li>string(50)

</li></ul> | \[Facilities]<ul><li>Unique identifier associated to the Facility

</li><li>Name of Facility

</li></ul> | 
| RespondMetadata\*<ul><li>NextCursor\*\*

</li><li>HasNext

</li></ul> | <ul><li>Base64

</li><li>True/False

</li></ul> | <ul><li>indicate the position of the next record not fetched into the list.Null if hasNext = False

</li><li>flag to indicate if there are more records matched the query parameter but not being fetched into the list.

</li></ul> | 


### Businesses Sample Object

```json
{
	"businessAccountId":"DSFit1",
	"name":"Northshore - Debitsuccess 24/7 Fitness",
	"penaltyFee":
					{
					  "amount": 10.00,
					  "payer":"Facility Pays"
					},
	"establishmentFee":
					{
					  "amount": 10.00,
					  "percent":50.00,
					  "payer":"Facility Pays"
					},
	"supportedPaymentMethods":
	[
					{
					  "paymentMethodType": "MasterCard"
					},
					{
					  "paymentMethodType": "Visa"
					},
					{
					  "paymentMethodType": "BankAccount"
					}
	],
	"business":
					{
					  "businessId":"3333333",
					  "name":"24/7 fitness"
					}
}

```


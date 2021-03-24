# Payment
The Account Payment API provides an interface for businesses (Facility Accounts) to accept payment for an account.As a result of a successful (authorized) payment, RecBatch, Docket, Trans and Payment will be created. A one-off PaySchedule will be created if required.


### Endpoints
See all [Payment API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5e324afe57963486220555b5?&tags=Payment&groupBy=tag).



| <span style="background-color: #FFF44F"> POST</span>  Payment | /account/creditcard | 
|  --- |  --- | 
| <span style="background-color: #E8F48C"> GET</span> Payment | /account/creditcard/{ExternalPaymentIdentifier} | 


### Create Payment


 **Environments** 



| [https://oc-test.debitsuccess.com/payments/v1.0](https://oc-test.debitsuccess.com/payments/v1.0) | 

 **On this page:** 


## Account Payment Object


|  **Parameter**  |  **Optional / Required**  |  **Format**  |  **Notes**  | 
|  --- |  --- |  --- |  --- | 
| AccountId | Required | String(15) | Account.AdfitNoOnly contains alpha numeric | 
| ExternalPaymentIdentifier | Required | String(50) | Must be unique per clientOnly contains alpha numeric and hyphen | 
| AccountHolderName | Required if CardType is not ‘Token’ | String(50) | Only restriction is on length | 
| CardNumber | Required if CardType is not ‘Token’ | String(20) | Only contains numeric | 
| CVC | Required if CardType is not ‘Token’ | String(4) | Only contains numeric | 
| CardType | Required | String(20) | VisaMasterCardTokenetc. | 
| ExpiryDate | Required if CardType is not ‘Token’ | String(7)“MM/yyyy” | Only contains numeric and '/' | 
| Token | Required if CardType is ‘Token’ | String(256) | Unique string value associated with PayMethod | 
| Amount | Required | Numeric 2 decimal points | Minimum amount is $1.00.Maximum amount is $10,000.00. (Can be configured) | 
| PaymentDescription | Optional | String(30) |  | 
| CreateOneOffCharge | Optional | Boolean | If ‘true’, a One-Off pay schedule will be createdThe default value is ‘false’ | 


### Account Payment Sample Object

```
{
	"accountId": "DEMO1234567",
	"externalPaymentIdentifier": "W3E4R5TY-5T54-76YT-78UY-DEFR435TGH67",
	"accountHolderName": "Test",
	"cardNumber": "4111111111111111111",
	"cvc": "123",
	"cardType": "visa",
	"expiryDate": "11/2022",
	"amount": 55.50,
	"paymentDescription": "Payment of $55.50 for testing",
	"createOneOffCharge": true
}

-- Using token
{
	"accountId": "DEMO1234567",
	"externalPaymentIdentifier": "W3E4R5TY-5T54-76YT-78UY-DEFR435TGH67",
	"cardType": "token",
	"token": "3CEB437E-C9AC-4D92-B06F-91AF64B913EA",
	"amount": 55.50,
	"paymentDescription": "Payment of $55.50 for testing",
	"createOneOffCharge": true
}
```



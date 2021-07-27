# Real Time Payment Widget

The Real Time Payment Widget allows customers to securely make real-time payments to your business. The widget can be embedded into your website and customized to match your product theme. The widget is made up of a JavaScript library that internally uses an iframe to capture credit card details. It then uses a Debitsuccess payment API to process payments.

>
The Real Time Payment Widget currently supports only casual payments. Support for account payments will be added in the future.

The default casual payment form:

![](https://drive.google.com/uc?export=view&id=1tkN8CSBIXyYfwYgeQgmE_TxZNvspc6fj) 

## Adding Real Time Payment Widget to a Web Page

The following steps will walk you through collecting payment using the casual payment widget.

### Step 1 - JavaScript library 

Add a link to the Debitsuccess javascript library on the page where the widget will be used, like:

```json
<script src="https://oc.debitsuccess.com/dspaymentwidget/dsRealTimePaymentWidget.js"></script>
```


### Step 2 - Initializing the Widget

In JavaScript code, the widget can be initialized as follows. 

>
It is recommended to initialize the widget once DOM has been fully loaded.


```json
var dsPaymentWidget;
document.addEventListener("DOMContentLoaded", function() {
    dsPaymentWidget = new DsRealTimePaymentWidget(
                      "auth_token_xxx",
                      "XXXX",  // Business Account ID
                      "https://oc-test.debitsuccess.com" // ds domain                     
                  );
});
```

`DsRealTimePaymentWidget` requires the following parameters when initialized.

|  **Parameter**  |  **Required**  |  **Description**  | 
|  --- |  --- |  --- | 
|  _authToken_  |  | get this token from [Debitsuccess Identity Server](https://debitsuccess.stoplight.io/docs/debitsuccess-api/docs/Introduction/2-Authentication.md) using your  _client secret_  and  _client ID_  | 
|  _businessAccountId_  |  | a unique identifier (string, Debitsuccess contract prefix) of the business customer belongs to | 
|  _domain_  | Optional | describes the environment the widget will be used against, possible values:  **OC-Test** https://oc-test.debitsuccess.com  **OC-Production** https://oc.debitsuccess.com (default) |

### Step 3 - Initialize casual payments form

```json
var casualPaymentOptions = {
    externalPaymentIdentifier: "<externalPaymentIdentifier>",
    paymentDescription: "<paymentDescription>",
    amount: 10.90
}
dsWidget.createCasualPaymentForm(casualPaymentOptions ,"payment-container", styles, labels, 650);

```

#### InitializeCasualPaymentForm

In initialize `CasualPaymentForm(casualPaymentOptions,containerElementId, styles, labels, width)` 

Where:

- *casualpaymentoptions* - javascript object with populated with casual payment API attributes.

- *containerElementId* - id of the parent element for iframe with the form;

- *styles* *(optional) - a string of custom CSS styles for the form;

- *labels* *(optional) - a JSON object with key-value pairs label id - label text;

- *width* *(optional) -  Maximum width of iframe in pixels, if it’s not provided default value is 350 px. Should be provided as an integer value

#### Casual Payment Options

Parameter | Required | Description
---------|----------|---------
 externalPaymentIdentifier | Required | A unique external payment identifier can later be used to retrieve the status of the payment ([Get - Casual Payment Status](https://debitsuccess.stoplight.io/docs/debitsuccess-api/PaymentsAPI.v1.json/paths/~1casual~1creditcard~1%7BexternalPaymentIdentifier%7D/get)). This identifier must be unique for every request. 
 paymentDescription | Optional | A free text field allows to store up to 40 characters.
 amount | required | Amount to be charged to the customer.

#### Form Style

For style customization, Debitsuccess accepts the following CSS properties:

```json
"margin", "margin-top", "margin-bottom", "margin-left", "margin-right",
"padding", "padding-top", "padding-bottom", "padding-left", "padding-right",
"color", "background-color",
"border",
"display", "border-radius",
"font", "font-weight", "font-size", "font-style", "font-family",
"text-align",
"width", "min-width", "max-width",
"height", "min-height", "max-height"

```
When you create a form and want to apply custom styles, they should be provided as the second parameter in the string representation, like so:

```json
dsPaymentWidget.createCasualPaymentForm(
           casualPaymentOptions,
          "card-container", 
          ".form-control{border:1px solid green;background:red;position:absolute;} #card-number{background:green;padding1:10px;}", 
          "");
```
#### Labels text replacement

The labels with the following IDs can be replaced as follows:
```json
"lbl-card-form-header",
"lbl-card-holder-name",
"lbl-card-number",
"lbl-card-expiry-date",
"lbl-card-cvc"
"lbl-card-amount"
"lbl-card-description"
```
When you create a form and want to replace labels' text with the custom ones, the information should be provided in JSON representation in the third parameter. Where the key is a label id and the value of the text you want to display, like so:

```json
dsPaymentWidget.createCasualPaymentForm(
          casualPaymentOptions
          "container", 
          "", 
          {
              "lbl-card-form-header": "Pay now",
              "lbl-card-holder-name": "Card Holder",
              "lbl-card-number": "Card Number",
              "lbl-card-expiry-date": "Card Expiry", 
              "lbl-card-cvc": "Cvc",
              "lbl-card-amount": "Amount",
              "lbl-card-description": "Desc"                          
          });
```
### Step 4 - Process Casual Payment

The widget provides the `MakeCasualPayment` to process casual payments for a business. This method returns a promise, which must be handled by the client. 

```json
dsPaymentWidget
  .processPayment()
  .then(function(paymentResponse) {
	// See https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/1596424197/Post+-+Make+Casual+Payment#Response for response format.        
   })
  .catch(function(err) {
	// See https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/1596424197/Post+-+Make+Casual+Payment#Response for response format.
	// Show errors returned from server to user.
   });
```
### Step 5 - Retrieve Payment Status

When the makeCasualPayment widget returns a successful payment response in the `Then catch block` use the `externalPaymentIdentifier` and call [GET- Casual Payment Status](https://debitsuccess.stoplight.io/docs/debitsuccess-api/PaymentsAPI.v1.json/paths/~1casual~1creditcard~1%7BexternalPaymentIdentifier%7D/get) to retrieve the payment response on the server-side.

>
We strongly recommend that GET- Casual Payment Status is called on the server-side. This will prevent any client-side response spoofing issues. The `externalPaymentIdentifier` should be store on the server-side and used to check for payment status.

```json
{
    "status": "authorised",
    "externalPaymentIdentifier": "b97d9688-1a07-4b35-ae54-28e32870f7cd"
}
```

Status Code | Description | 
---------|----------|
 authorized | Successful Transaction | 
 declined | Transaction declined | 
 declined_insufficient_funds | Insufficient funds is an issue that occurs when an account does not have adequate capital to satisfy a payment demand | 
 declined_card_expired | Payment has been declined due to an expired card.
declined_refer_to_card_issuer |Refer to Issuer. The customer's bank (Card Issuer) has indicated there is a problem with the card number. The customer should contact their bank or the customer should use an alternate card. |
 processing |Payment has been accepted for processing. But the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place. In this scenario, you must poll the Get Casual Payment status endpoint (Step 5 - Retrieve Payment Status) to retrieve the payment status code. It is recommend to retry retrieving the status code 5 times within a 2-minute duration. If the status code still is processing after retrying, please contact Debitsuccess support. |

## Response Simulation

NZ/AU: The following cards can be used to generate different types of status for testing purpose.

**authorised**
- Card Type: Visa

- Card Number: 4444333322221111

- Expiry Date: 04/25

- Card Holder: AUTHORISED

**declined**
- Card Type: Visa

- Card Number: 4444333322221111

- Expiry Date: 04/25

- Card Holder: REFUSED

**declined_insufficient_funds**
- Card Type: AmericanExpress

- Card Number: 343434343434343

- Expiry Date: 04/25

- Card Holder: REFUSED51

** declined_refer_to_card_issuer**

- Card Type: AmericanExpress

- Card Number: 343434343434343

- Expiry Date: 04/25

- Card Holder: REFUSED5

## Handling Error Message
The widget does not perform any client-side validation. Validation occurs on the server-side when the makeCasualPayment function is called. The widget returns error messages in the catch block. The integrator must review all the error messages returned and handle them accordingly. 

### HTTP 201
Successful Transaction
```json
{
  "status": "authorised",
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
}
```
Transaction declined
```json
{
  "status": "declined",
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc",
}
```
Insufficient funds is an issue that occurs when an account does not have adequate capital to satisfy a payment demand

```json
{
  "status": "declined_insufficient_funds", 
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc",
}
```
Payment has been declined due to an expired card

```json
{
  "status": "declined_card_expired", 
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
}
```
Do not honour means that the customer's card issuing bank has declined the transaction. This is the most common message provided by card-issuing banks when a transaction fails their authorisation process. Ask your customer to contact their bank to check there are no issues with their card.
```json
{
  "status": "declined_do_not_honour", 
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
}
```
Refer to Issuer. The customer's bank (Card Issuer) has indicated there is a problem with the card number. The customer should contact their bank or the customer should use an alternate card.

```json
{
  "status": "declined_refer_to_card_issuer", 
  "externalPaymentIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
}
```
### HTTP 202

Payment has been accepted for processing. But the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place. In this scenario, the client must poll the URL returned in the "location" header of the response to retrieve the payment status code. The client must retry retrieving the status code 5 times within a 2-minute duration. If the status code still is processing after retrying. The client should contact Debitsuccess support.

```json
{
  "status": "Processing",  
  "externalIdentifier": "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
}
```
### HTTP 403
Occurs when you don't have access to the endpoint.
```json
{
    "errorCode": "required_claims",   
    "message": "Unable to process this request due to insufficient client claims.",     
    "errors": [           
       {               
           "claim": "The name of the claim required."           
       }      
    ]
}
```
Occurs when the identity server-client does not have access to the business Id provided in the request
```json
{
  "errorCode": "business_permission",   
  "message": "Unable to process this request due to insufficient business permission."   
}
```
### HTTP 422- Unprocessable Entity

```json
{
  "errorCode": "legal_address", 
  "message": "No Legal Address found on file. Please contact Debitsuccess."
},
{
  "errorCode": "merchant_details", 
  "message": "Cannot find valid merchant details configured. Please contact Debitsuccess."
},
{
  "errorCode": "business_id", 
  "message": "Cannot find business that matches the business id provided."
},
{
  "errorCode": "business_commission", 
  "message": "Cannot find commission details configured for this business. Please contact Debitsuccess."
},
{
  "errorCode": "card_type", 
  "message": "Cannot find any card types configured for this business. Please contact Debitsuccess."
},
{
  "errorCode": "card_not_accepted", 
  "message": "The selected payment method is not supported by this business."
}
```
### HTTP 400- Validation errors
```json
{
  "field": "CardHolderName", 
  "message": "'CardHolderName' should not be empty."
},
{
  "field": "CardHolderName", 
  "message": "The length of 'CardHolderName' must be 50 characters or fewer. You entered <> characters."
},
{
  "field": "PaymentDescription", 
  "message": "The length of 'PaymentDescription' must be 40 characters or fewer. You entered <> characters."
},
{
  "field": "CardType", 
  "message": "'CardType' should not be empty."
},
{
  "field": "CardType",
  "message": "Invalid CardType provided. Please use one of the supported cards for this BusinessID"
},
{
  "field": "CardNumber", 
  "message": "Invalid card number" 
},
{
  "field": "Cvc", 
  "message": "'Cvc' should not be empty."
},
{
  "field": "Cvc", 
  "message": "Invalid CVC number"
},
{
  "field": "ExpiryDate", 
  "message": "'ExpiryDate' should not be empty."
},
{
  "field": "ExpiryDate", 
  "message": "Invalid ExpiryDate Format. Please use MM/yy."
},
{
  "field": "Amount", 
  "message": "Amount should not be empty."
},
{
  "field": "Amount", 
  "message": "Card payment amount must be greater than or equal to $1 and less than your configured maximum value"
},
{
  "field": "BusinessId", 
  "message": "'BusinessId' should not be empty."
},
{
  "field": "BusinessId", 
  "message": "'The length of 'BusinessId' must be 6 characters or fewer. You entered <> characters."
},
{
  "field": "ExternalPaymentIdentifier", 
  "message": "'ExternalPaymentIdentifier' should not be empty."
},
{
 "field": "ExternalPaymentIdentifier", 
 "message": "The length of 'ExternalPaymentIdentifier' must be 50 characters or fewer. You entered <> characters."
}
```

## Related Articles
- [Data for Test Environment](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/989890688/Data+for+Test+Environment)

- [Create customer accounts for testing](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1549369452/Create+customer+accounts+for+testing)

- [Statuses in Debitsuccess Systems](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1492877598/Statuses+in+Debitsuccess+Systems)
# Payment Capture Widget

The Payment Capture Widget allows you to securely capture payment details (credit card and bank account) by embedding it in your website and save payment details in Debitsuccess systems. This widget triggers the internal [Create PaymentMethod](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5e4317913b44f651f411dc64?&groupBy=tag) API to create the payment method into Debitsuccess.


>
The [Create PaymentMethod](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5e4317913b44f651f411dc64?&groupBy=tag) API is intended for internal use only. If you decide to capture credit cards yourself and pass them through the API then you would be required to be PCI certified as opposed to doing a PCI self-assessment.


## Adding payment capture widget

1. Add a link to DS javascript library on the page where the widget will be used, like



```json
<script src="https://oc.debitsuccess.com/dswidget/dsPaymentFormWidget.js"></script>
```

 2. In your javascript code, you need to initiate a new instance of  _DsPaymentFormWidget_ and pass the following parameters:



|  **Parameter**  |  **Required**  |  **Description**  | 
|  --- |  --- |  --- | 
|  _authToken_  |  | get this token from [Debitsuccess Identity Server](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/986809101/Authentication) using your  _client secret_  and  _client ID_  | 
|  _businessAccountId_  |  | a unique identifier (string, DS contract prefix) of the business customer belongs to | 
| customerId  | Optional | a unique identifier (integer) of the customer the payment method will be captured for | 
|  _domain_  | Optional | describes the environment the widget will be used against, possible values:  **OC-Test** https://oc-test.debitsuccess.com  **OC-Production** https://oc.debitsuccess.com | 
|  _accountId_  | Optional | a unique identifier (string, DS account reference) of the account a new payment method should be attached to | 


```js
var dsWidget = new DsPaymentFormWidget(
                        "auth_token_xxx",
                        "XXXX",  // Business Account ID
                        {
                            "customerId": "123456" // your Customer ID
                            "domain": "https://oc-test.debitsuccess.com",
                            "accountId": 654321
                        }
                    );
```
 3. Initiate the widget.


> It is recommend to initiate the widget after the DOM content is loaded.


```js
var var dsWidget;
document.addEventListener("DOMContentLoaded", function() {
    dsWidget = new DsPaymentFormWidget(
                      "auth_token_xxx",
                      "XXXX",  // Business Account ID
                      {
                          "customerId": "123456" // your Customer ID
                          "domain": "https://oc-test.debitsuccess.com",
                          "accountId": 654321
                      }
                  );
});
```
 4. Subscribe to [events ](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/1357742205/Payment+Capture+Widget#Events)emitted from the widget to get a notification on your website. 


```js
dsWidget.subscribe(function(d) {
		if(d.type === "stateUpdated") {
			// update UI elements based on validation results, for example
			submitButton.disabled = ! d.valid;
		}
		
		if(d.type === "savePaymentMethodError") {
			// handled via Promise
		}
		
		if(d.type === "savePaymentMethodProcessing") {
			// may display hourglass or something
		}					
		
		if(d.type === "savePaymentMethodSuccess") {
			//handled via Promise
		}
	});
```
5. The widget doesn’t have its own submit button. In order to save information on the form, you need to call the  _createPaymentToken_ method of the widget. The method returns a promise which you need to handle in your code.


```
dsWidget.createPaymentToken()
    .then(function(paymentToken) {
        console.log(paymentToken);
        submitButton.disabled = false;
    })
    .catch(function(err) {
        console.error(err.errorJSON ? JSON.stringify(err.errorJSON) : err.errorStatus || "ERROR");
        submitButton.disabled = false;
    });
```

## Using credit card capture form
If you want to add a form for capturing credit card details to your page you need to call method  _createCardCaptureForm(containerElementId, styles, labels, width)_ 

Where:


*  _containerElementId_  - id of the parent element for iframe with the form;


*  _styles*(optional)_ - a string of custom CSS styles for the form;


*  _labels*(optional)_  - a JSON object with key-value pairs label id - label text;


*  _width*(optional) -_ Maximum width of iframe in pixels, if it’s not provided default value is 350 px. Should be provided as an integer value.




```
dsWidget.createCardCaptureForm("card-container", styles, labels, 650);
```

## Using bank account capture form
If you want to add a form for capturing bank account information to your page you need to call method  _createBankCaptureForm(containerElementId, country, styles, labels, width)_ where:


*  _containerElementId_  - id of the parent element for iframe with the form;


*  _country_  - the ISO Alpha 3 code of the country, bank account belongs to;


*  _styles*(optional) - a string of custom CSS styles for the form;_ 


*  _labels*(optional) - a JSON object with key-value pairs label id - label text;_ 


*  _width*(optional) -_ Maximum width of iframe in pixels, if it’s not provided default value is 350 px. Should be provided as an integer value.




```
dsWidget.createBankCaptureForm("bank-container", "AUS", styles, customBankLabels, 450);
```

## Customing the payment capture widget
Debitsuccess Payment Capture widget supports CSS style customization and labels text replacement. By default, the Payment Capture forms are displayed as below:


<!--
type: tab
title: AUS and NZ Credit Card Details Capture Form
-->

 ![](https://drive.google.com/uc?export=view&id=1xthBX73Jhr9rIBBltqccnB26kko9S6vv) 



<!--
type: tab
title: NZ Bank Account Details Capture Form
-->

![](https://drive.google.com/uc?export=view&id=1In38dCAZgBz0J_muhGCnESH4i8IAWVp8)


<!--
type: tab
title: AUS Bank Account Details Capture Form
-->

![](https://drive.google.com/uc?export=view&id=1sV1cQWQD3oOYdCngPnrQzPsfbAWEvPPo)


<!-- type: tab-end -->



CSS styles customizationFor style customization, Debitsuccess accepts the following CSS properties:


```js
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


```
dsWidget.createCardCaptureForm(
          "card-container", 
          ".form-control{border:1px solid green;background:red;position:absolute;} #card-number{background:green;padding1:10px;}", 
          "");
```

### Labels text replacement
The labels with the following IDs can be replaced as follows:


```js
// card elements
"lbl-card-form-header",
"lbl-card-holder-name",
"lbl-card-number",
"lbl-expiry-date",
// bank elements
"lbl-bank-form-header",
"lbl-account-holder",
"lbl-account-number"
```
When you create a form and want to replace labels' text with the custom ones, the information should be provided in JSON representation in the third parameter. Where the key is a label id and the value the text you want to display, like so:


```js
dsWidget.createCardCaptureForm(
          "card-container", 
          "", 
          {
              "lbl-card-holder-name": "Ingoa",
              "lbl-card-number": "Tau Kaari",
              "lbl-expiry-date": "Ra Whakamutunga",
              "lbl-card-form-header": "Kia Ora!"
          });
```

## Events
The Payment Capture widget emits javascript events for communicating with a parent website. All the events have a property  _type_  describes what event it is.


### Subscribing to events
Subscribe to events emitted by the widget


```js
dsWidget.subscribe(function(event){
  console.log(event);
},"stateUpdated");
```

### Unsubscribing from the widget events
Removes an existing subscription


```js
dsWidget.unsubscribe("stateUpdated");
```
Types of eventsa) Initialized eventThen a capture form is initialized the  _initialized_ event is emitted with the following structure. Where  _minWidth_ & _minHeight_  represent the minimum size of the form that has been created.


```
{
  "type":"initialized",
  "minWidth":300,
  "minHeight":323
}
```
b) State updated eventThis event is emitted when the validation state is changed. When the form is loaded the default value is false. When the form is changing state to valid the following event is exposed.


```
{
    "type":"stateUpdated",
    "valid":true,
    "errorMessage":""
}
```
If you enter a card number which is not supported the following event is raised:


```
{
     "type":"stateUpdated",
     "valid":false,
     "errorMessage":"Unsupported card type"
}
```
If you are using as a constructor parameter country which is not supported, for the bank account capture form, the following event is exposed when you try to enter the bank account number:

The event with the following error message is applicable only for the bank account capture form.


```json
{
    "type": "stateUpdated",
    "valid": false,
    "errorMessage": {
        "AccountHolderError": "The account holder name is invalid"
        "AccountNumberError": "The account number is invalid",
        "BsbError": "Bsb is invalid",
        "CountryError": "Unsupported country"
    }
}
```
c) Save payment method processing eventWhen you call createPaymentToken() method, the following event is exposed:


```js
{
    "type":"savePaymentMethodProcessing"
}
```
d) Save payment method success eventIf the payment method was successfully saved, based on you the widget parameters you will have either of the following events come back:


* If  **customerId**  is provided:




```json
{
    "type":"savePaymentMethodSuccess",
    "token": {
                "paymentMethodToken":"W3E4R5TY-5T54-76YT-78UY-DEFR435TGH67",
                "holderName":"TestName",
                "paymentMethodType":"CreditCard",
                "number":"**** 1111",
                "cardType":"visa",
                "cardExpiryDate":"11/22"
             }
}
```

* If  **customerId** is not provided, you will get a one time token as shown below. To get a permanent token, you need to use PATCH customer API and provide this OneTimePaymentMethodToken:




```json
{
    "type":"savePaymentMethodSuccess",
    "token": {
                "oneTimePaymentMethodToken":"8525e997-c7b6-412b-896d-0a46257501eb",
                "tokenExpiryDateTime":"2020-10-21T21:44:23.701Z"
             }
}
```
If a token was created without specifying a customer id, later on, when the customer is created, you will need to associate this oneTimePaymentMethodToken using  **_PATCH_** Customer call


```js
var data = JSON.stringify({"oneTimePaymentMethodToken":"8525e997-c7b6-412b-896d-0a46257501eb"});

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function() {
  if(this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("PATCH", "https://oc-test.debitsuccess.com/customerservices/v1.0/customers/{{yourCustomerId}}/paymentMethods");
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("Authorization", "Bearer authToken");

xhr.send(data);
```
e) Save payment method error eventIf you send a payment form which is invalid state the event of the following structure is raised:


```js
{
    "type":"savePaymentMethodError",
    "errorStatus":"400",
    "errorJSON":{
                    "Error":"Validation failed."
                 }
}
```
If widget validation was bypassed then an error message from API might be exposed in the event


```js
{
    "type":"savePaymentMethodError",
    "errorStatus":400,
    "errorJSON": {
                      "errorCode":"validation",
                      "message":"Unable to process request due to validation errors.",
                      "errors":[{
                                     "field":"holderName",
                                     "message":"HolderName is required."
                                  },
                                  {
                                      "field":"paymentMethodType",
                                      "message":"PaymentMethodType is required."
                                   }]
                   }
}
```
f) Configuration error when initializing the widgetIf you do not provide  **businessAccountId,** a configurationError event with a message “businessAccountId is invalid.” is returned.


```js
{"type":"configurationError",
"errorStatus":"400",
"errorJSON":
  {
    "Error":"businessAccountId is invalid."
  }
}
```

## Response structure

### HTTP 201 - Created

```json
{
	"token": "W3E4R5TY-5T54-76YT-78UY-DEFR435TGH67",
	"number": "**** 4444" (last 4 digits of bank account number or credit card)
}
```

### HTTP 400 - Bad Request

```json
{
    "errorCode": "validation",
    "message": "Invalid request",
    "errors": [
        {
            "field": "AccountId",
            "message": "AccountId is required."
        }
    ]
}
```

### HTTP 401 - Unauthorized

### HTTP 403 - Forbidden

```json
# when the client does not have access to the account
{
    "errorCode": "business_permission",
    "message": "Unable to process this request due to insufficient business permission."   
}

# when the client does not have access to the endpoint
{
    "errorCode": "required_scopes",
    "message": "Unable to process this request due to insufficient client scopes.",
    "requiredScopes": [
        "CapturePayMethod"
    ]
}
```

### HTTP 500 -Internal Server Error




*****



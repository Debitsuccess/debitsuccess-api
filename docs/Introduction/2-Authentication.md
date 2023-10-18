# Authentication 

Debitsuccess supports [client credentials](https://tools.ietf.org/html/rfc6749#section-1.3.4) flow for authentication. After you receive your credentials, `Client_ID` and `Client_Secret` from us, use the  HTTP POST request to **/identity/connect/token** to obtain your JWT token also known as API Key.

## OAuth 2.0 Client Credentials Flow 
![](https://drive.google.com/uc?export=view&id=1CbINB1zSVaIgocEuRkcNFnsyp3_S6F38)


1. Your app authenticates with the Debitsuccess Identity Server using its Client ID and Client Secret.


1. The Debitsuccess Identity Server validates the Client ID and Client Secret and responds with an Access Token (JWT Token)


1. Your application must use the Access Token to call a Web service (API) on behalf of itself.


1. The web service retrieves the public key to validate the access token.


1. The web service responds with requested data.



To integrate your web server application with the Debitsuccess Identity Server, follow the below steps:


### Prerequisites
Ensure that you have your `client_id` and `client secret` provided by our Debitsuccess team handy. You may request credentials by contacting our [account management team](https://www.debitsuccess.co.nz/). This `client ID` is unique to your application.

To check whether the identity server is up and running navigate to the configuration endpoint.

[https://oc-sbox.debitsuccess.com/identity/.well-known/openid-configuration](https://oc-sbox.debitsuccess.com/identity/.well-known/openid-configuration)


### 1. Retrieve an access token
To receive an access token, the client POSTs an API call to Debitsuccess Identity Server, with the values for the client ID and client secret. In addition, the parameter grant_type=client_credentials must be passed as a query parameter.

**Request Parameters**
* Method: <span style="background-color:skyblue; color:white">  POST</span>


* URL: https://oc-sbox.debitsuccess.com/identity/connect/token


* Content-Type: application/x-www-form-urlencoded


* Response Type: json



|  **Input Parameter**  |  **Required/Optional**  |  **Format**  |  **Remark**  | 
|  --- |  --- |  --- |  --- | 
| Client_ID | Required | ########-####-####-####-############ where # is alphanumeric | Unique identifier for a client provided by Debitsuccess. | 
| Client_Secret | Required | 64 bit | Client secret key provided by Debitsuccess. | 
| Grant_Type | Required | stringclient_credentials | Denotes the flow you are using. Always use client_credentials | 
| scope | Optional | Space-separated string | The name of the API that access token will be generated for. If the scope is not provided by Debitsuccess, you can ignore this field in the request body. Also if the scope is not provided the token will contain all available scopes for this client_id.| 




```json
POST https://oc-sbox.debitsuccess.com/identity/connect/token

Headers:

Content-Type: application/x-www-form-urlencoded

Body: grant_type=client_credentials&client_id=xxxxxxx&

client_secret=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

Scope: CasualCreditCard
```
**Response 200- Successful Request**

In exchange for these credentials, the Debitsuccess authorization server issues access tokens called bearer tokens that you use for authorization when you make REST API requests. A bearer token enables you to complete actions on behalf of, and with the approval of, the resource owner.



|  **Output Parameter**  |  **Format**  |  **Remark**  | 
|  --- |  --- |  --- | 
| Access_Token | sample:     "eyJhbGciOiJSUzI1NiIsImtpZCI6IkE4ODFDQzdBNDM4MEUyRDM5N0EwQjNGMERGNDF GOTg1MDYzRkU1RkIiLCJ0eXAiOiJKV1QiLCJ4NXQiOiJxSUhNZWtPQTR0T1hvTFB3MzBINWhRA” | It represents the authorization of a specific application to access specific parts of user data and uniquely identifies the client login session.  | 
| Expires_In | Integer in seconds, example 1800, 3600 | Represents the number of seconds that the access token will be valid. | 
| Token_Type | "Bearer" | A bearer token means that the bearer of the access token can access authorized resources without further identification. The access token must always be appended with the term “Bearer” when you call any Debitsuccess REST API. E.g. Bearer \[access_token]| 


```json
{

  "access_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjExODhlZTc5NjIzNTVlODYwNzUwMWIzMGY2Y2QzZjBmIiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MTE2NTIwODEsImV4cCI6MTUxMTY1NTY4MSwiaXNzIjoiaHR0cDovL2xvY2FsaG9zdDozMDAw

                   MiIsImF1ZCI6WyJodHRwOi8vbG9jYWxob3N0OjMwMDAyL3Jlc291cmNlcyIsIk9NRyJdLCJjbGllbnRfaWQiOiI1ZjFiMWQ2Ny02NDlhLTRmYzMtYjkzMC1iMzExOTFjZjZmMTEiLCJjbGllbnRfVXNlcklkIjoiMTIzNCIsInNjb3BlIjpbIk9NRyJdfQ.Mlnd0RZhW8tp

                   8Ktj7_KuxViFAzyeYLMl7SdnVbKAFNPh74Z9Ib4u8kGMvz0ZFnx62_CaMpSPEwE6wHdFBTeBKvYKN5h1PjnJrrSh9J2S4a3PsCnnlLrhfO6sNBHzZzAlQhGMQei2GHQufiOyWtrYSfK8R4Ye1ULeysTRkfrWxk_fZ3Brm_vFh5J43EbTHe8NSgIXbobyN7brVFjntNZskJ

                   Sj4QUaw8Fz1npwZSNHF8XpOMZIEWAL2uOWUPm18Op-1IDOOj04eZAsFoHL5gb_pNqGph5SejTqjSbpbabMalJlaxvJrA1NNFxbGAMGXWR0ocJZvmlIYRebrueZk5yGg",

 "expires_in": 3600,

 "token_type": "Bearer"

}
```
**Error message 400- Bad Request, Request validation error**

The response message will vary depending on the cause.


```json
{
error	string
example: unsupported_grant_type,invalid_scope,invalid_client.
The error response can include any value that is discribed in the example.

}
```
 ### 2. Call an API with the access token
 
 The token lives for the configured time in the authorization server, when the token expires the API should respond with a 401 telling the client to get a new token.

To call the API, the token should be added to the request in the Authorization header on the form as shown in the below example:

**Request format**


```json
GET https://oc-sbox.debitsuccess.com/customerservice/accounts/{accountId}

Headers:

content-type: application/json; charset=utf-8

Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IjExODhlZTc5NjIzNTVlODYwNzUwMWIzMGY2Y2QzZjBmIiwidHlwIjoiSldUIn0.eyJuYmYiOjE1MTE2NTUyNzQsImV4cCI6MTUxMTY1ODg3NCwiaXNzIjoiaHR0cDovL2xvY2F
saG9zdDozMDAwMiIsImF1ZCI6WyJodHRwOi8vbG9jYWxob3N0OjMwMDAyL3Jlc291cmNlcyIsIk9NRyJdLCJjbGllbnRfaWQiOiI1ZjFiMWQ2Ny02NDlhLTRmYzMtYjkzMC1iMzExOTFjZjZmMTEiLCJjbGllbnRfVXNlcklkIjoiMTIzNCIsInN
jb3BlIjpbIk9NRyJdfQ.NVON-z-Dli5AjSR91M6PR4jGUh9SyCej0sAaC0ClBIQbo9Eez7LP7ZGeVU2_UfGdv6mAmmuBrWKlC3LvAxXpavFACw0cSbtG_ayLwIyfkc1PGHZO1F8xqMdskD6vM6h704cuZ7XCE3otIYM-1IEvuEV7dl_83MtFX9cF
K3QsDwjYlgwAWUBH7IxKDJCAXXqf4PqZY53jr1tjMDBgINRsl0iCjG83X9pvzf0pa9i5bLfFHmDLgagGpqdm7-GwTDNgzAx28gXzlzWFSuuWkikzTw7F7Mi7O91u3Su3dHZ79hc0YxoIJ7q7pMss1bhdYiGiPCQ-GNTkljeG5vatPZvSxQ
```


*******

**JWT Token validation**  JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA. We will be using RSA to sign the token. RS256 (RSA Signature with SHA-256) is an asymmetric algorithm, and it uses a public/private key pair: the identity server provider has a private (secret) key used to generate the signature, and the consumer of the JWT gets a public key to validate the signature. Since the public key, as opposed to the private key, doesn't need to be kept secured, the identity server makes it easily available for consumers to obtain from the [https://oc-sbox.debitsuccess.com/identity/.well-known/openid-configuration/jwks](https://oc-sbox.debitsuccess.com/identity/.well-known/openid-configuration/jwks) URL. To read more about JWT tokens please visit [https://jwt.io/introduction/](https://jwt.io/introduction/).



*****

>Identity URLs:                                     
>OC-Test : https://oc-test.debitsuccess.com/Identity          
>OC-SBOX : https://oc-sbox.debitsuccess.com/Identity
>Production : https://oc.debitsuccess.com/Identity

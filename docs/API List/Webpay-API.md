{
  "openapi" : "3.0.0",
  "info" : {
    "title" : "Web Pay API",
    "description" : "Debitsuccess Webpay API provides an interface for Webpay integration. This API supports posting credit card payments for customers who have their BPay CRN registered with Debitsuccess. \n\n## Authentication \nPlease visit [Debitsuccess Identity Service](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/986809101/Authentication) \n\n## Test Envrionment\n\n[https://oc-test.debitsuccess.com/{Api Endpoint}](https://oc-test.debitsuccess.com/Payments/v1.0/casual/creditcard) \n\n## Immutable Requests\nThe API supports immutable requests across all endpoints that are used to create payments. This immutability is enforced by using a unique ExternalPaymentIdentifier + Identity Server Client Id. \nFor example, if a request to create a payment fails due to a declined transaction or unknown server error. The API will reject subsequent requests with the same ExternalPaymentIdentifier and for the same Identity server client. \n\nThe immutability prevents integration partners from accidentally performing the same payment request twice preventing potential double billing issues. \n\nHow you create unique ExternalPaymentIdentifier is up to you, but we suggest using business ID + a V4 UUIDs or another appropriately random string together to generate a unique ExternalPaymentIdentifier.  \n\n\n### Response\n\n  This API uses conventional HTTP response codes to indicate the success or failure of an \n  API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate \n  an error that failed given the information provided (e.g., a required parameter was omitted, a \n  request validation failed, etc.), and some codes in the 5xx range indicate an error with Api's\n  servers.\n  \n  Following is a list of supported HTTP codes in this Api.\n  - 200 Ok - Get\n  \n    Returned by Get endpoint to indicate that the request was successful. \n  \n  - 201 Created - Post\n  \n    Returned by HTTP post method to indicate that a payment resource has been created. The response \n    will contain the payment status code. \n  \n  - 202 Accepted - Post\n  \n    This message indicates that a payment has been accepted for processing. But the processing has not\n    been completed. The request might or might not eventually be acted upon, as it might be disallowed\n    when processing actually takes place. In this scenario, the client must poll the URL returned in \n    the \"location\" header of the response to retrieve the payment status code. The client must retry \n    retrieving the status code 5 times. If the status code still is \n    processing after retrying. The client should contact Debitsuccess support. The client should not ignore this error and resubmit another payment. Doing so could potentially double bill the customer.\n  \n  - 400 Bad Request - Post\n    \n    Throughout the API the HTTP code 400 is used when the request was \n    unacceptable, often due to missing a required field or validation errors based on the data\n    provided in the request body. The validation errors can be displed to the end-user. \n  \n  - 422 Unprocessable Entity - Post\n    \n    Returned when the client application or the facility account is not configured for real-time \n    casual payments. All facility accounts must be configured with the payment gateways before \n    they can process any type of payments. In the event this error occurs the integration partner must\n    contact Debitsuccess to review/configure the facility accounts.\n    \n  - 401 Unauthorized - Get/Post\n    \n    Occurs when an Unauthorized request is made to a secure endpoint. A valid access token is expected\n    by all the secured endpoints via a ```Authorization``` header. See [Debitsuccess Identity Service](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/986809101/Authentication) for more \n    information in obtaining valid JWT tokens. The client must retry the request by obtaining a valid access token from the identity service.\n\n  - 403 Forbidden - Get/Post\n  \n    This indicates that the authenticated request does not have sufficient claims for an endpoint. \n   \n  - 409 Conflict - Post\n    \n    The request could not be completed due to a conflict with the external payment identifier.\n    \n  - 429 Too Many Requests - Get\n    \n    Occurs with rate limit is hit by the client.\n  \n  - 500  Internal Server Error\n  \n    Typically occurs when something goes wrong on Api back end (These are rare).\n  \n  - 503 Service Unavailable\n  \n    Occurs when the API is currently unavailable typically due to a scheduled outage. \n\n### Response Headers\n  \n   The following additional headers are added to specific response message.\n   \n  - location - returned in 201 and 202. The value of this header contains the URL that can be used to retrieve the payment status.\n  \n  - x-correlation-id - included in all response messages. This is used internally in Debitsuccess to track the path of the realtime payment request. The API consumer is expected to provide a correlation Id for all support requests.   \n  \n### Response Simulation\n  \n  \*\*NZ/AU\*\*: The following cards can be used to generate different types of status for testing purpose.\n  \n  - Status - authorised\n    \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4111111111111111 | \*\*Expiry Date\*\*: 04/35\n  \n  - Status - declined \n    \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999236 | \*\*Expiry Date\*\*: 04/35\n  \n  - Status - declined_insufficient_funds \n  \n    \*\*Card Type\*\*: MasterCard | \*\*Card Number\*\*: 5431111111111228 | \*\*Expiry Date\*\*: 04/35\n    \n  - Status - declined_card_expired \n  \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999996 | \*\*Expiry Date\*\*: 04/10\n  \n  - Status - not_submitted \n  \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999202 | \*\*Expiry Date\*\*: 04/35\n\n",
    "contact" : {
      "email" : "TestAPI.Support@debitsuccess.com"
    },
    "version" : "3.0"
  },
  "servers" : [ {
    "url" : "/"
  } ],
  "tags" : [ {
    "name" : "Casual Payments"
  } ],
  "paths" : {
    "/payments/v1.0/webpay/creditcard/" : {
      "get" : {
        "tags" : [ "Casual Payments" ],
        "description" : "This endpoint can be used to retrieve the payment status for all the casual payments submitted via the Post endpoint.\n",
        "parameters" : [ {
          "name" : "externalPaymentIdentifier",
          "in" : "path",
          "description" : "External Payment Identifier reference used to identify the payment.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        }, {
          "name" : "authorization",
          "in" : "header",
          "description" : "JWT token using Bearer authorization scheme. See [Debitsuccess Identity Service ](https://app.swaggerhub.com/apis/debitsuccess/DebitsuccessIdentity/1.0.0) on how to generate the authorization token.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        } ],
        "responses" : {
          "200" : {
            "description" : "The payment request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http200)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/CasualPaymentResponseSuccess"
                }
              }
            }
          },
          "401" : {
            "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            }
          },
          "403" : {
            "description" : "Forbidden - Occurs when the client does not have sufficient claims to access this endpoint. Or when the identity server client does not have access to the business this request is being made for. see - [ List of claims required for this request](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources) see - [ Additional errorCodes returned](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/PermissionErrorList"
                }
              }
            }
          },
          "404" : {
            "description" : "Not Found - The requested resource could not be found",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Not-Found"
                }
              }
            }
          },
          "500" : {
            "description" : "Internal Server Error - Something went wrong on our end (These are rare).",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/ServerError"
                }
              }
            }
          }
        }
      },
      "post" : {
        "tags" : [ "Casual Payments" ],
        "description" : "This endpoint processes credit card casual payments. Casual payments are recorded at the business level (Facility Account). The details of the customer making the payments are not recorded.",
        "parameters" : [ {
          "name" : "authorization",
          "in" : "header",
          "description" : "JWT token using Bearer authorization scheme. See [Debitsuccess Identity Service ](https://app.swaggerhub.com/apis/debitsuccess/DebitsuccessIdentity/1.0.0) on how to generate the authorization token.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string"
          }
        } ],
        "requestBody" : {
          "content" : {
            "application/json" : {
              "schema" : {
                "$ref" : "#/components/schemas/PaymentRequest"
              }
            }
          }
        },
        "responses" : {
          "201" : {
            "description" : "The payment request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http201)",
            "headers" : {
              "location" : {
                "$ref" : "#/components/headers/location"
              },
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/CasualPaymentResponseSuccess"
                }
              }
            }
          },
          "202" : {
            "description" : "Payment has been accepted for processing.  But the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place. In this scenario, the client must poll the URL returned in the \"location\" header of the response to retrieve the payment status code. The client must retry retrieving the status code 5 times within a 2-minute duration. If the status code still is processing after retrying. The client should contact Debitsuccess support.",
            "headers" : {
              "location" : {
                "$ref" : "#/components/headers/location"
              },
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/CasualPaymentResponseAccepted"
                }
              }
            }
          },
          "400" : {
            "description" : "Bad Request - Request failed due to validation errors, the response lists the field in the request that did not pass the validation. The client can directly show these errors to the end-users. see- [List of validation errors](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http400)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/ValidationErrorList"
                }
              }
            }
          },
          "401" : {
            "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            }
          },
          "403" : {
            "description" : "Forbidden - Occurs when the client does not have sufficient claims to access this endpoint. Or when the identity server client does not have access to the business this request is being made for. see - [ List of claims required for this request](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources) see - [ Additional errorCodes returned](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/PermissionErrorList"
                }
              }
            }
          },
          "409" : {
            "description" : "The request could not be completed due to a conflict with the current state of the target resource.",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/Conflict"
                }
              }
            }
          },
          "422" : {
            "description" : "Payment processing failed. see - [for all possible responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http422)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/UnprocessableEntitySchema"
                }
              }
            }
          },
          "500" : {
            "description" : "Internal Server Error - Something went wrong on our end (These are rare).",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/ServerError"
                }
              }
            }
          }
        }
      }
    }
  },
  "components" : {
    "schemas" : {
      "PaymentRequest" : {
        "required" : [ "amount", "bpayReferenceNumber", "businessId", "cardHolderName", "cardNumber", "cardType", "cvc", "expiryDate", "externalPaymentIdentifier" ],
        "type" : "object",
        "properties" : {
          "cardHolderName" : {
            "type" : "string",
            "example" : "John Doe"
          },
          "cardNumber" : {
            "type" : "string",
            "example" : "4111111111111111"
          },
          "cvc" : {
            "type" : "string",
            "example" : "321"
          },
          "cardType" : {
            "type" : "string",
            "description" : "supported card types- AmericanExpress, MasterCard, Visa",
            "example" : "Visa"
          },
          "expiryDate" : {
            "type" : "string",
            "example" : "02/19"
          },
          "amount" : {
            "type" : "number",
            "description" : "The amount to be charged. Please note, amount will be truncated to 2 decimal places",
            "format" : "currency",
            "example" : 10.25
          },
          "bpayReferenceNumber" : {
            "type" : "string",
            "description" : "Bpay reference number that will determine business that is receiving the payment.",
            "example" : "abc"
          },
          "businessId" : {
            "type" : "string",
            "description" : "Debitsuccess business identifier that is receiving the payment.",
            "example" : "abc"
          },
          "externalPaymentIdentifier" : {
            "type" : "string",
            "description" : "A unique external payment identifier. Note, this is unique across all Debitsuccess customers. The API consumer is responsible for generating a unique identifier",
            "example" : "b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
          }
        }
      },
      "CasualPaymentResponseSuccess" : {
        "type" : "object",
        "properties" : {
          "status" : {
            "type" : "string",
            "example" : "authorised"
          },
          "externalPaymentIdentifier" : {
            "type" : "string",
            "example" : "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
          }
        }
      },
      "CasualPaymentResponseAccepted" : {
        "type" : "object",
        "properties" : {
          "status" : {
            "type" : "string",
            "example" : "Processing"
          },
          "externalPaymentIdentifier" : {
            "type" : "string",
            "description" : "ExternalPaymentIdentifier - The first half of the ExternalPaymentIdentifier identifies the business id.",
            "example" : "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
          }
        }
      },
      "CasualPaymentResponsePaymentRequired" : {
        "type" : "object",
        "properties" : {
          "status" : {
            "type" : "string",
            "example" : "Declined"
          },
          "externalPaymentIdentifier" : {
            "type" : "string",
            "example" : "ABC-b5645c56-943f-4562-ab2c-9aedf3c0b1dc"
          },
          "message" : {
            "type" : "string",
            "description" : "User-friendly response message from Payment gateway.",
            "example" : "Failed to process the request."
          }
        }
      },
      "UnprocessableEntitySchema" : {
        "type" : "object",
        "properties" : {
          "errorCode" : {
            "type" : "string",
            "example" : "bpayReferenceNumber"
          },
          "message" : {
            "type" : "string",
            "description" : "User-friendly response message from Payment gateway.",
            "example" : "Cannot find a business that matches the bpayReferenceNumber provided."
          }
        }
      },
      "PermissionError" : {
        "type" : "object",
        "properties" : {
          "claim" : {
            "type" : "string",
            "example" : "The name of the claim required."
          }
        }
      },
      "ServerError" : {
        "type" : "object",
        "properties" : {
          "message" : {
            "type" : "string",
            "example" : "Something went wrong while processing your request. We’re sorry for the trouble. We’ve been notified of the error and will correct it as soon as possible. Please try your request again in a moment."
          }
        }
      },
      "Not-Found" : {
        "type" : "object",
        "properties" : {
          "message" : {
            "type" : "string",
            "example" : "The requested resource could not be found."
          }
        }
      },
      "Conflict" : {
        "type" : "object",
        "properties" : {
          "errorCode" : {
            "type" : "string",
            "example" : "external_payment_identifier"
          },
          "message" : {
            "type" : "string",
            "example" : "The external payment identifier provided has already been used."
          }
        }
      },
      "ValidationError" : {
        "type" : "object",
        "properties" : {
          "field" : {
            "type" : "string",
            "example" : "amount"
          },
          "message" : {
            "type" : "string",
            "example" : "amount is required"
          }
        }
      },
      "ValidationErrorList" : {
        "type" : "object",
        "properties" : {
          "message" : {
            "type" : "string",
            "example" : "invalid request"
          },
          "errorCode" : {
            "type" : "string",
            "description" : "This code can be either invalid_request or validation. invalid_request indicates that the client provided ExternalPaymentIdentifier that does not match the format. Validation can be displayed to the end users. These include invalid information such as invalid credit card number no expiry date etc.",
            "example" : "validation"
          },
          "errors" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/ValidationError"
            }
          }
        }
      },
      "PermissionErrorList" : {
        "type" : "object",
        "properties" : {
          "errorCode" : {
            "type" : "string",
            "example" : "required_claims"
          },
          "message" : {
            "type" : "string",
            "example" : "Unable to process this request due to insufficient client claims."
          },
          "errors" : {
            "type" : "array",
            "items" : {
              "$ref" : "#/components/schemas/PermissionError"
            }
          }
        }
      }
    },
    "responses" : {
      "Success-Casual-Payment-Response-Ok" : {
        "description" : "The payment request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http200)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/CasualPaymentResponseSuccess"
            }
          }
        }
      },
      "Success-Casual-Payment-Response" : {
        "description" : "The payment request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http201)",
        "headers" : {
          "location" : {
            "$ref" : "#/components/headers/location"
          },
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/CasualPaymentResponseSuccess"
            }
          }
        }
      },
      "Accepted-Casual-Payment-Response" : {
        "description" : "Payment has been accepted for processing.  But the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place. In this scenario, the client must poll the URL returned in the \"location\" header of the response to retrieve the payment status code. The client must retry retrieving the status code 5 times within a 2 minute duration. If the status code still is processing after retrying. The client should contact Debitsuccess support.",
        "headers" : {
          "location" : {
            "$ref" : "#/components/headers/location"
          },
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/CasualPaymentResponseAccepted"
            }
          }
        }
      },
      "Required-Casual-Payment-Response" : {
        "description" : "Payment processing failed. see - [for all possible responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http402)",
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/CasualPaymentResponsePaymentRequired"
            }
          },
          "headers" : {
            "x-correlation-id" : {
              "$ref" : "#/components/headers/x-correlation-id"
            }
          }
        }
      },
      "Unprocessable-Entity-Response" : {
        "description" : "Payment processing failed. see - [for all possible responses](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http422)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/UnprocessableEntitySchema"
            }
          }
        }
      },
      "Forbidden" : {
        "description" : "Forbidden - Occurs when the client does not have sufficient claims to access this endpoint. Or when the identity server client does not have access to the business this request is being made for. see - [ List of claims required for this request](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources) see - [ Additional errorCodes returned](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-ApiResources)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/PermissionErrorList"
            }
          }
        }
      },
      "Not-Found" : {
        "description" : "Not Found - The requested resource could not be found",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/Not-Found"
            }
          }
        }
      },
      "Conflict" : {
        "description" : "The request could not be completed due to a conflict with the current state of the target resource.",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/Conflict"
            }
          }
        }
      },
      "Server-Error" : {
        "description" : "Internal Server Error - Something went wrong on our end (These are rare).",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/ServerError"
            }
          }
        }
      },
      "Unauthorised-Error" : {
        "description" : "Unauthorized - Occurs when the authorization token provided is either expired or invalid.",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        }
      },
      "Validation-Error" : {
        "description" : "Bad Request - Request failed due to validation errors, the response lists the field in the request that did not pass the validation. The client can directly show these errors to the end-users. see- [List of validation errors](https://debitsuccess.atlassian.net/wiki/spaces/RIDE/pages/500433563/RealTimePayment+API+Overview#RealTimePaymentAPIOverview-Http400)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/ValidationErrorList"
            }
          }
        }
      }
    },
    "parameters" : {
      "Authorization" : {
        "name" : "authorization",
        "in" : "header",
        "description" : "JWT token using Bearer authorization scheme. See [Debitsuccess Identity Service ](https://app.swaggerhub.com/apis/debitsuccess/DebitsuccessIdentity/1.0.0) on how to generate the authorization token.",
        "required" : true,
        "style" : "simple",
        "explode" : false,
        "schema" : {
          "type" : "string"
        }
      }
    },
    "headers" : {
      "location" : {
        "description" : "URL that can be used to retrieve the payment status",
        "style" : "simple",
        "explode" : false,
        "schema" : {
          "type" : "string",
          "example" : "Get - https://oc-test.debitsuccess.com/Payments/v1.0/realtime/cardpayments/TST-443508918"
        }
      },
      "x-correlation-id" : {
        "description" : "A unique identifier used to track the path this request internally in Debitsuccess.",
        "style" : "simple",
        "explode" : false,
        "schema" : {
          "type" : "string",
          "example" : "0HLD8JO11CCGR:00000001"
        }
      }
    }
  }
}

*****

[[category.storage-team]] 
[[category.confluence]] 

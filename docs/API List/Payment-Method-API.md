{
  "openapi" : "3.0.0",
  "info" : {
    "title" : "Payment Method Configuration API",
    "description" : "The Debitsuccess PayMethod Configuration API provides an interface to retrieve the Pay method types configured for particular businesses. Pay method types consist of credit card types and bank account. \n\n## Test Envrionment\n\n[https://oc-test.debitsuccess.com/{API Endpoint}](https://oc-test.debitsuccess.com/Payments/v1.0/casual/creditcard) \n\n\n## Authentication \nPlease visit [Debitsuccess Identity Service](https://debitsuccess.atlassian.net/wiki/spaces/DDE/pages/986809101/Authentication)  \n\n### Response\n\n  This API uses conventional HTTP response codes to indicate the success or failure of an \n  API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate \n  an error that failed given the information provided (e.g., a required parameter was omitted, a \n  request validation failed, etc.), and some codes in the 5xx range indicate an error with API's\n  servers.\n  \n  Following is a list of supported http codes in this API.\n  - 200 Ok - Get\n  \n    Returned by Get endpoint to indicate that the request was successful. \n  \n  - 400 Bad Request - Post\n    \n    Throughout the API the http code 400 is used when the request was \n    unacceptable, often due to missing a required field or validation errors based on the data\n    provided in the request body. The validation errors can be displed to the end-user. \n  \n  - 401 Unauthorized - Get/Post\n    \n    Occurs when an Unauthorized request is made to a secure endpoint. A valid access token is expected\n    by all the secured endpoints via an ```Authorization``` header. See [Debitsuccess Identity Service](https://app.swaggerhub.com/apis/debitsuccess/DebitsuccessIdentity/1.0.0) for more \n    information in obtaining valid JWT tokens. The client must retry the request by obtaining a valid access token from the identity service.\n\n  - 429 Too Many Requests - Get\n    \n    Occurs with rate limit is hit by the client.\n  \n  - 500  Internal Server Error\n  \n    Typically occurs when something goes wrong on API back end (These are rare).\n  \n  - 503 Service Unavailable\n  \n    Occurs when the API is currently unavailable typically due to a scheduled outage. \n\n### Response Headers\n  \n   The following additional headers are added to specific response message.\n   \n  - location - returned in 201 and 202. The value of this header contains the URL that can be used to retrieve the payment status.\n  \n  - x-correlation-id - included in all response messages. This is used internally in Debitsuccess to track the path of the realtime payment request. The API consumer is expected to provide a correlation id for all support requests.   \n  \n### Response Simulation\n\ \n  \*\*NZ/AU\*\*: The following cards can be used to generate different types of status for testing purpose.\n  \n  - Status - authorised\n    \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4111111111111111 | \*\*Expiry Date\*\*: 04/35\n  \n  - Status - declined \n    \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999236 | \*\*Expiry Date\*\*: 04/35\n  \n  - Status - declined_insufficient_funds \n  \n    \*\*Card Type\*\*: MasterCard | \*\*Card Number\*\*: 5431111111111228 | \*\*Expiry Date\*\*: 04/35\n    \n  - Status - declined_card_expired \n  \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999996 | \*\*Expiry Date\*\*: 04/10\n  \n  - Status - not_submitted \n  \n    \*\*Card Type\*\*: Visa | \*\*Card Number\*\*: 4999999999999202 | \*\*Expiry Date\*\*: 04/35\n    \n",
    "contact" : {
      "email" : "TestAPI.Support@debitsuccess.com"
    },
    "version" : "1.0"
  },
  "servers" : [ {
    "url" : "/"
  } ],
  "tags" : [ {
    "name" : "Pay Method Configuration"
  } ],
  "paths" : {
    "/payments/v1.0/paymethods" : {
      "get" : {
        "tags" : [ "Pay Method Configuration" ],
        "description" : "This endpoint retrieves all active paymethod types for the particular business identified by either businessId (Contract Prefix) or Debitsuccess internal facility Id parameter. Note, you must provide at least one parameter (bussinessId or facilityId)in the request.\n",
        "parameters" : [ {
          "name" : "bussinessId",
          "in" : "query",
          "description" : "Debitsuccess bussiness identifier (Contract Prefix).",
          "required" : false,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          }
        }, {
          "name" : "facilityId",
          "in" : "query",
          "description" : "Debitsuccess internal facility identifier.",
          "required" : false,
          "style" : "form",
          "explode" : true,
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
            "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "type" : "array",
                  "items" : {
                    "$ref" : "#/components/schemas/PayMethodResponseList"
                  }
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
    },
    "/payments/v1.0/paymethods/{paymethodtype}" : {
      "get" : {
        "tags" : [ "Pay Method Configuration" ],
        "description" : "This endpoint retrieves the paymethod configuration information based on the paymethod type provided in the request path. \n",
        "parameters" : [ {
          "name" : "paymethodtype",
          "in" : "path",
          "description" : "Paymethod type that is supported by Debitsuccess.",
          "required" : true,
          "style" : "simple",
          "explode" : false,
          "schema" : {
            "type" : "string",
            "example" : "VI,DI,BA etc"
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
            "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "$ref" : "#/components/schemas/PayMethodResponse"
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
      }
    },
    "/payments/v1.0/paymentprocessorcardtypes" : {
      "get" : {
        "tags" : [ "Pay Method Configuration" ],
        "description" : "This endpoint retrieves the mapping between Debitsuccess card type and a payment processor (Vantiv, Dps) the payment processor specific card type are used when submitting a payment request. Example - DS card type = AM - Vantiv card type = AX\n",
        "parameters" : [ {
          "name" : "processorname",
          "in" : "query",
          "description" : "The name of the payment processors used by Debitsuccess (Vantiv, DPS).",
          "required" : true,
          "style" : "form",
          "explode" : true,
          "schema" : {
            "type" : "string"
          }
        }, {
          "name" : "cardtype",
          "in" : "query",
          "description" : "Debitsuccess internal card type.",
          "required" : true,
          "style" : "form",
          "explode" : true,
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
            "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
            "headers" : {
              "x-correlation-id" : {
                "$ref" : "#/components/headers/x-correlation-id"
              }
            },
            "content" : {
              "application/json" : {
                "schema" : {
                  "type" : "array",
                  "items" : {
                    "$ref" : "#/components/schemas/PaymentProcessor"
                  }
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
      }
    }
  },
  "components" : {
    "schemas" : {
      "PayMethodResponseList" : {
        "type" : "object",
        "properties" : {
          "methodType" : {
            "type" : "string",
            "description" : "The type of paymethod (CC - Credit Card or BA - Bank Account).",
            "example" : "CC"
          },
          "methodSubType" : {
            "type" : "string",
            "description" : "The credit card type of the paymethod",
            "example" : "VI"
          },
          "networkName" : {
            "type" : "string",
            "description" : "Name of the network that issued the card type.",
            "example" : "Visa"
          },
          "creditAllowed" : {
            "type" : "boolean",
            "description" : "Is credit card allowed or not.",
            "example" : true
          },
          "debitAllowed" : {
            "type" : "boolean",
            "description" : "Is debit card allowed or not.",
            "example" : true
          },
          "prepaidAllowed" : {
            "type" : "boolean",
            "description" : "Is prepaid card allowed or not.",
            "example" : false
          },
          "validationRules" : {
            "type" : "array",
            "description" : "Validation rules that can be used to determine whether a card number matches this paymethod.",
            "items" : {
              "$ref" : "#/components/schemas/ValidationRules"
            }
          }
        }
      },
      "PayMethodResponse" : {
        "type" : "object",
        "properties" : {
          "methodType" : {
            "type" : "string",
            "description" : "The type of paymethod (CC - Credit Card or BA - Bank Account).",
            "example" : "CC"
          },
          "methodSubType" : {
            "type" : "string",
            "description" : "The credit card type of the paymethod",
            "example" : "VI"
          },
          "networkName" : {
            "type" : "string",
            "description" : "Name of the network that issued the card type.",
            "example" : "Visa"
          },
          "validationRules" : {
            "type" : "array",
            "description" : "Validation rules that can be used to determine whether a card number matches this paymethod.",
            "items" : {
              "$ref" : "#/components/schemas/ValidationRules"
            }
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
      "PaymentProcessor" : {
        "type" : "object",
        "properties" : {
          "PaymentProcessorCardType" : {
            "type" : "string",
            "description" : "The card type that is configured for payment processor.",
            "example" : "AX"
          },
          "PaymentProcessorName" : {
            "type" : "string",
            "description" : "Name of the payment processor.",
            "example" : "Vantiv"
          }
        }
      },
      "ValidationRules" : {
        "type" : "object",
        "properties" : {
          "regex" : {
            "type" : "string",
            "description" : "Regex value that can be used to validate card number.",
            "example" : "^(4)"
          },
          "purpose" : {
            "type" : "string",
            "description" : "Defines the purpose of the regex value. In this example, the corresponding regex can be used to determine whether a card number is visa card type.",
            "example" : "CardType"
          }
        }
      }
    },
    "responses" : {
      "PaymentProcessor-Response" : {
        "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "type" : "array",
              "items" : {
                "$ref" : "#/components/schemas/PaymentProcessor"
              }
            }
          }
        }
      },
      "Success-PayMethod-Response-List" : {
        "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "type" : "array",
              "items" : {
                "$ref" : "#/components/schemas/PayMethodResponseList"
              }
            }
          }
        }
      },
      "Success-PayMethod-Response" : {
        "description" : "The request was successful. see - [List of responses](https://debitsuccess.atlassian.net/wiki/spaces/SDT/pages/803176544/Payment+Method+Configuration+API#PaymentMethodConfigurationAPI-WebAPI)",
        "headers" : {
          "x-correlation-id" : {
            "$ref" : "#/components/headers/x-correlation-id"
          }
        },
        "content" : {
          "application/json" : {
            "schema" : {
              "$ref" : "#/components/schemas/PayMethodResponse"
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

# HTTP Response 

The service uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the 2xx range indicate success, codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a request validation failed, etc.), and some codes in the 5xx range indicate an error with APIs servers.

The API returns errors in JSON format in the following structure:


```json
{
  "errorCode": "access_denied",
  "message": "Unable to process this request as you do not have access to the customer associated to this request."
}
```

|  **Response Code**  |  **Response Code Description**  |  **Error Code**  |  **Message**  | 
|  --- |  --- |  --- |  --- | 
| 200 | OK |  |  | 
| 400 | Bad Request |  |  | 
| 401 | Unauthorized |  | Authorization has been denied for this request | 
| 403 | Forbidden | customer_access_denied | Unable to process this request as you do not have access to the customer associated to this request | 
| 404 | Not Found |  | The requested resource could not be found. | 
| 429 | Too many requests |  | You have exceeded the maximum limit of request allowed. Please try your request again in a moment | 
| 500 | Internal Server Error |  | Something went wrong while processing your request. We’re sorry for the trouble. We’ve been notified of the error and will correct it as soon as possible. Please try your request again in a moment. | 
| 503 | Service Unavailable |  | The API is currently unavailable due to a scheduled outage – please try again soon | 



*****


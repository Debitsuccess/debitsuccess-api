




### Endpoints
See all [Suspension Schedule APIs](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5ddb3c9f2e24240b5236e6a5?tags=Schedules-Suspension&pattern=&groupBy=).



| POSTYellow Schedule (Suspension) | /accounts/{accountId}/suspensionSchedules | 
|  --- |  --- | 
| GETGreen Schedule (Suspension) | /accounts/{accountId}/suspensionSchedules/{scheduleId} | 
| GETGreen Schedules (Suspension) | /accounts/{accountId}/suspensionSchedules | 
| PATCH Schedule (Suspension) | /accounts/{accountId}/suspensionSchedules/{scheduleId} | 
| DELETERed Schedule (Suspension) | /accounts/{accountId}/suspensionSchedules/{scheduleId} | 


## Workflows

### Create Suspension Schedule workflow
 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## Suspension Schedules Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| ScheduleId | integer | Unique schedule number associated with the suspension schedule created | 
| AccountId | string(15) | System generated reference id associated to the Account of the suspension schedule created. | 
| SuspensionScheduleStartDate | "YYYY-MM-DD" | Date (in UTC) when this suspension schedule starts | 
| SuspensionScheduleEndDate | "YYYY-MM-DD" | Date (in UTC) when this suspension schedule ends. | 
| SuspensionFee | numeric(8,2) | Installment amount to be paid for this suspension schedule | 
| Frequency | Enum- One-Off, Weekly, Fortnightly,Four-Weekly, Monthly, Bi-Monthly, Quarterly | Frequency of payment for this suspension schedule. | 
| ScheduleDescription | string(50) | Description associated to the created suspension schedule | 
| ExternalScheduleId | string(50) | External identifier of the created suspension schedule | 


### Suspension Schedules Sample Object

```json
{ 
   "suspensionScheduleStartDate":"2020-01-31",
   "suspensionScheduleEndDate":"2020-02-31",
   "suspensionFee":50.00,
   "frequency":"monthly",
   "numberOfPayments":null,
   "scheduleDescription":"Suspension schedule Jan-Feb",
   "externalScheduleId":"S125810"
}
```


*****

[[category.storage-team]] 
[[category.confluence]] 

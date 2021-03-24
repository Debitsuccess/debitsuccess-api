# One-Off Schedules

### Endpoints
See all [One-off Schedule APIs](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5ddddd7330e1bcdcaf336cb8?tags=Schedules-OneOff&pattern=&groupBy=).



| POSTYellow Schedule (One-off ) | /accounts/{accountId}/oneOffSchedules | 
|  --- |  --- | 
| GETGreen Schedule (One-off ) | /accounts/{accountId}/oneOffSchedules/{scheduleId} | 
| GETGreen Schedules (One-off ) | /accounts/{accountId}/oneOffSchedules | 
| DELETERed Schedule (One-off ) | /accounts/{accountId}/oneOffSchedules/{scheduleId} | 


## Workflows
 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


## One-off Schedules Object


|  **Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| ScheduleId | integer | Unique schedule number associated with the Recurring Schedule created | 
| AccountId | string(15) | System generated reference id associated to the Account of the Recurring Schedule created. | 
| DueDate | YYYY-MM-DD | Date (in UTC) when this recurring schedule starts | 
| Amount | numeric(8,2) | Installment amount to be paid for this recurring schedule | 
| ScheduleDescription | string(50) | Description associated to the created recurring schedule | 
| ExternalScheduleId | string(50) | External identifier of the created recurring schedule | 


### One-off Schedules Sample Object

```json
{
   "scheduleId":"12345678",
   "accountId":"AILL056H6",
   "dueDate":"2020-01-31",
   "amount":50.00,
   "scheduleDescription":"One-off Schedule",
   "externalScheduleId":"S125810"
}
```

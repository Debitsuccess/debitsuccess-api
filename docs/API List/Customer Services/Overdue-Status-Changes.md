Retrieve the details of overdue statuses or amount changesbased on the specified date range.


### Endpoints
See [OverdueStatusChanges API](https://oc-debitsuccess.portal.azure-api.net/docs/services/Mock/operations/5e1778c773c4b5d0db9def9c?tags=OverdueStatusChanges&pattern=&groupBy=tag).



| GETGreen OverdueStatusChanges | /overdueStatusChanges | 



 **Environments** 



| [https://oc-test.debitsuccess.com/CustomerServices/v1.0](https://oc-test.debitsuccess.com/CustomerServices/v1.0) | 

 **On this page:** 


### Overdue Status Changes Object


|  **Output Parameter**  |  **Format**  |  **Description**  | 
|  --- |  --- |  --- | 
| BusinessAccountId | string(6) | Facility Account associated to the account extracted | 
| AccountId | string(15) | System generated reference no associated with the Account. | 
| AccountExternalId | string(50) | External reference no associated with the Account. | 
| FromOverdueStatus | integer | Previous account's overdue status | 
| FromOverdueStatusChangeDateTime | "YYYY-MM-DDThh:mm:ss.ssssZ" | Previous account's overdue status changed date | 
| FromOverdueAmount | numeric(10,2) | Previous account's overdue amount | 
| ToOverdueStatus | integer | New account's overdue status | 
| ToOverdueStatusChangeDateTime | "YYYY-MM-DDThh:mm:ss.ssssZ" | New account's overdue status changed date | 
| ToOverdueAmount | numeric(10,2) | Newaccount's overdue amount | 


### Overdue Status Changes Sample Object

```json
{
"overdueStatusChanges":[
       {
              "businessAccountId":"DSFit1",
              "accountId":"AILL056H6",
              "AccountExternalId":"ABC123",
              "fromOverdueStatus":0,
              "fromOverdueAmount":"0.00",
              "fromOverdueStatusChangeDateTime":"2019-01-01T08:11:55Z",
              "toOverdueStatus":1,
              "toOverdueAmount":"10.00",
              "toOverdueStatusChangeDateTime":"2019-01-02T08:11:55Z"
       },
       {
              "businessAccountId":"DSFit1",
              "accountId":"AILL056H8",
              "AccountExternalId":"ABC122",
              "fromOverdueStatus":1,
              "fromOverdueAmount":"100.00",
              "fromOverdueStatusChangeDateTime":"2019-01-01T08:11:55Z",
              "toOverdueStatus":0,
              "toOverdueAmount":"0.00",
              "toOverdueStatusChangeDateTime":"2019-01-02T08:11:55Z"
       }
],
"responseMetadata":{
       "nextCursor":"TmV4dEl0ZW1JZDoz",
       "hasNext":true
       }
}
```


*****

[[category.storage-team]] 
[[category.confluence]] 

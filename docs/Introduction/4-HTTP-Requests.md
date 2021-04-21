# HTTP Requests

## Filtering
The _$filter_ query string parameter allows clients to filter a collection of resources that are addressed by a request URL. The expression specified with _$filter_ is evaluated for each resource in the collection, and only items where the expression evaluates to true are included in the response. Resources for which the expression evaluates to false or to null, or which reference properties that are unavailable due to permissions, are omitted from the response.

Example: return all Products whose Price is less than $10.00


```
GET http://debitsuccess.com/DsCoreApi/v1.0/accounts?$filter=AdfitNo eq TST13522
```
The value of the _$filter_ option is a Boolean expression.


### Filter Operations
Services that support _$filter_ SHOULD support the following minimal set of operations.



|  **Operator**  |  **Description**  |  **Example**  | 
|  --- |  --- |  --- | 
| Comparison Operators |  |  | 
| eq | Equal | city eq 'Auckland' | 
| ne | Not equal | city ne 'Auckland' | 
| gt | Greater than | price gt 20 | 
| ge | Greater than or equal | price ge 10 | 
| lt | Less than | price lt 20 | 
| le | Less than or equal | price le 100 | 
| Logical Operators |  |  | 
| and | Logical and | price le 200 and price gt 3.5 | 
| or | Logical or | price le 3.5 or price gt 200 | 
| not | Logical negation | not price le 3.5 | 
| Grouping Operators |  |  | 
| ( ) | Precedence grouping | (priority eq 1 or city eq 'Auckland') and price gt 100 | 


### Examples
The following examples illustrate the use and semantics of each of the logical operators.

Example: all accounts with a name equal to 'John'


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=name eq 'John'
```
Example: all accounts with a name not equal to 'John'


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=name ne 'John'
```
Example: all accounts with the name 'John' that also have a age less than 2 years:


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=name eq 'John' and age lt 2
```
Example: all accounts that either have the name 'John' or have a age less than :


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=name eq 'John' or age lt 2
```
Example : all accounts that have the name 'John' or 'Doe' and have a price less than 2.55:


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=(name eq 'John' or name eq 'Doe') and age lt 2
```

###  **Expression Evaluating Orde** r


|  **Group**  |  **Operator**  |  **Description**  | 
|  --- |  --- |  --- | 
| Grouping | ( ) | Precedence grouping | 
| Unary | not | Logical Negation | 
| Relational | gt | Greater Than | 
|  | ge | Greater than or Equal | 
|  | lt | Less Than | 
|  | le | Less than or Equal | 
| Equality | eq | Equal | 
|  | ne | Not Equal | 
| Conditional AND | and | Logical And | 
| Conditional OR | or | Logical Or | 




## Sorting Collections
The results of a collection query MAY be sorted based on property values. The property is determined by the value of the _$orderBy_ query parameter.

The value of the _$orderBy_ parameter contains a comma-separated list of expressions used to sort the items. A special case of such an expression is a property path terminating on a primitive property.

The expression MAY include the suffix "asc" for ascending or "desc" for descending, separated from the property name by one or more spaces. If "asc" or "desc" is not specified, the service MUST order by the specified property in ascending order.

NULL values MUST sort as "less than" non-NULL values.

Items MUST be sorted by the result values of the first expression, and then items with the same value for the first expression are sorted by the result value of the second expression, and so on. The sort order is the inherent order for the type of property.

Sorting should be available on list responses. sorting can be very beneficial when combined with pagination.


### Interpreting a sorting expression
Sorting parameters MUST be consistent across pages, as both client and server-side paging is fully compatible with sorting.

If a service does not support sorting by a property named in a _$orderBy_ expression, the service MUST respond with an error message as defined in the Responding to Unsupported Requests section.


### Examples



```
GET https://debitsuccess.com/core/v1.0/accounts?$orderBy=name
```
Will return all accounts sorted by name in ascending order.

For example:


```
GET https://debitsuccess.com/core/v1.0/accounts?$orderBy=name desc
```
Will return all accounts sorted by name in descending order.

Sub-sorts can be specified by a comma-separated list of property names with OPTIONAL direction qualifier.

For example:


```
GET https://debitsuccess.com/core/v1.0/accounts?$orderBy=name desc,startDate
```
Will return all accounts sorted by name in descending order and a secondary sort order of startDate in ascending order.

Sorting MUST compose with filtering such that:


```
GET https://debitsuccess.com/core/v1.0/accounts?$filter=name eq 'john'&$orderBy=startDate
```
Will return all accounts whose name is john sorted in ascending order bystartDate.




## Pagination
nextCursor: Is used to indicate the first record to be fetched in the next retrieval if we wanted to continue to fetch more records.

limit



RESTful APIs that return collections MAY return partial sets. Consumers of these services MUST expect partial result sets and correctly page through to retrieve an entire set.

Client-driven pagination MUST be supported by RESTful APIs.Client-driven paging enables clients to request only the number of resources that it can use at a given time.

Sorting and Filtering parameters MUST be consistent across pages, because both client- and server-side paging is fully compatible with both filtering and sorting.


### Client-driven paging
Clients MAY use _$top_ and _$skip_ query parameters to specify a number of results to return and an offset into the collection.

The server SHOULD honour the values specified by the client; however, clients MUST be prepared to handle responses that contain a different page size.

When both _$top_ and _$skip_ are given by a client, the server SHOULD first apply _$skip_ and then _$top_ on the collection.

Note: If the server does not support _$top_ and/or _$skip_ , the server MUST return an error to the client informing about it instead of just ignoring the query options. This will avoid the risk of the client making assumptions about the data returned.

Filtering, Sorting and Pagination operations MAY all be performed against a given collection. When these operations are performed together, the evaluation order MUST be:


1.  **Filtering** . This includes all range expressions performed as an AND operation.


1.  **Sorting** . The potentially filtered list is sorted according to the sort criteria.


1.  **Pagination** . The materialized paginated view is presented over the filtered, sorted list. This applies to both server-driven pagination and client-driven pagination.



 **Constrains** 


1. The server side MUST restrict/default $top to 100 records. If $top is more than 100 then the server must respond with an HTTP 400 error.


1. All pagination responses must include the count of total items as custom header 'X-Total-Items'.


1. $skip must default to 0



 **Examples** 
```
Pagination
GET http://debitsuccess.com/core/v1.0/accounts?$top=10&$skip=2
[
  ''
]
header:
X-Total-Items: 500

Pagination + filtering & sorting

GET http://debitsuccess.com/core/v1.0/accounts?$filter=name eq 'John'$orderBy=name desc$top=10&$skip=2
[
 ''
]
header:
X-Total-Items: 200
```



## Valid Date Format

### dateTimefields
Use theyyyy-MM-ddTHH:mm:ss.SSSZformat to specifydateTimefields.

Where,


* yyyyis the four-digit year


* MMis the two-digit month (01-12)


* ddis the two-digit day (01-31)


* 'T' is a separator indicating that time-of-day follows


* HHis the two-digit hour (00-23)


* mmis the two-digit minute (00-59)


* ssis the two-digit seconds (00-59)


* SSSis the optional three-digit milliseconds (000-999)


* 'Z' is the reference UTC timezone



When a timezone is added to a UTC dateTime, the result is the date and time in that timezone. For example, 2020-10-10T12:00:00+05:00 is 2020-10-10T07:00:00Z and 2020-10-10T00:00:00+05:00 is 2020-10-09T19:00:00Z. 

The dateTimes in input parameters should always be in UTC. The dateTimes returned from our API are also in UTC.


### datefields
Use theyyyy-MM-ddformats to specifydatefields in local timezone, not UTC.

*****

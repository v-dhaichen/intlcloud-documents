
## API Description
The API LookupEvents is used to search the operation log for relevant operation information.
Domain name for API access: `cloudaudit.api.qcloud.com`


## Request Parameters
The following request parameter list only provides the API request parameters.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| EndTime | Yes | DateTime | End time |
| LookupAttributes | Yes | Array | Array of attributes, which supports only one element. If it is not specified, the first ten entries are returned. |
| MaxResults | No | Number | Number of entries returned. If it is not specified, 10 entries are returned. A maximum 50 entries are supported. |
| NextToken | No | String | It is used when more logs are loaded. |
| StartTime | Yes | DateTime | Start time |

LookupAttributes is composed of the following parameters:

 | Parameter Name | Required | Type | Description |
|---------|---------|---------|--------|
| AttributeKey | No |	String | Search types (enumeration values), including Username (user name), EventName (event name), ResourceType (resource type), ResourceName (resource name), EventSource (event source), and EventId (Event ID). |
| AttributeValue | No |	String	| Value |
## Response Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Events | Array | Array of events |
| NextToken | String | It is used when more logs are loaded. |

Events is composed of the following parameters:


| Parameter Name | Type | Description |
|---------|---------|---------|
| CloudAuditEvent | String | Event string |
| EventId | String | Event ID |
| EventName | String | Event name |
| EventSource | String | Event source |
| EventTime | String | Event time |
| SecretId | String | Access key |
| EventRegion | String | Region |
| ErrorCode | Number | Error code. 0: normal; other error codes: error. |
| RequestID | String | Request ID |
| SourceIPAddress | String | Source IP address |
| Resources | Object | Resource |
| Username | String | User name. Primary account: root; sub-account: sub-account ID; role user: roleUser. |

Resources is composed of the following parameters:

| Parameter Name | Type | Description |
|---------|---------|---------|
| ResourceName | String | Resource name |
| ResourceType | String |	Resource type |



## Example
### Request

```
{
   "EndTime": Number,
   "LookupAttributes": [
      {
         "AttributeKey": "String",
         "AttributeValue": "String"
      }
   ],
   "MaxResults": Number,
   "NextToken": "String",
   "StartTime": Number
}
```
### Response

```
{
   "Events": [
      {
         "CloudAuditEvent": "String",
         "EventId": "String",
         "EventName": "String",
         "EventSource": "String",
         "EventTime": "String",
         "SecretId":"String",
         "EventRegion":"String",
         "ErrorCode":Number,
         "EventTime":"String",
         "RequestID":"String",
         "SourceIPAddress":"String",
         "Resources": [
            {
               "ResourceName": "String",
               "ResourceType": "String"
            }
         ],
         "Username": "String"
      }
   ],
   "NextToken": "String"
}
```


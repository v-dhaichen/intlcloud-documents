## 1. API Description

API request domain name: organization.tencentcloudapi.com.

This API is used to obtain Tencent Cloud Organization member information.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/850/38722).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: GetOrganizationMember |
| Version | Yes | String | Common parameter; the version of this API: 2018-12-25 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| MemberUin | Yes | Integer | Organization member UIN |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Uin | Integer | Organization member UIN |
| Name | String | Organization member name |
| Remark | String | Remarks |
| JoinTime | Timestamp | Joined date |
| NodeId | Integer | Organizational unit ID |
| NodeName | String | Organizational unit name |
| ParentNodeId | Integer | Parent organizational unit ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId must be provided when troubleshooting issues. |

## 4. Example

### Example 1: Obtaining TCO Member Information

#### Input Example

```
https://organization.tencentcloudapi.com/?Action=GetOrganizationMember
&MemberUin=123
&<Common Request Parameters>
```

#### Output Example

```
{
  "Response": {
    "Uin": 1,
    "Name": "aa",
    "Remark": "",
    "JoinTime": "2019-10-10 00:00:00",
    "NodeId": 1,
    "NodeName": "aa",
    "ParentNodeId": 0,
    "RequestId": "fae840be-2b30-47ae-93b7-df5610168eff"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=organization&Version=2018-12-25&Action=GetOrganizationMember)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/850/38725#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| ResourceNotFound.NodeNotExist | The Tencent Cloud organizational unit does not exist. |
| ResourceNotFound.OrganizationNotExist | The Tencent Cloud Organization does not exist. |

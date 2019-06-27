﻿## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API disconnects the upstream connection. This action is resumable.

Default API request rate limit: 100 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459)..

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DropLiveStream |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| StreamName | Yes | String | Stream name |
| DomainName | Yes | String | Your acceleration domain name |
| AppName | Yes | String | Application name |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

This API can be called when the upstream of a VJ needs to be paused for some reasons.

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=DropLiveStream
&DomainName=5000.livepush.myqcloud.com
&AppName=live
&StreamName=stream1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "8e50cdb5-56dc-408b-89b0-31818958d424"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=DropLiveStream)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes


The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.CallOtherSvrError | Error calling internal service. |
| InternalError.ConfigNotExist | The configuration does not exist. |
| InternalError.GetBizidError | Error getting user account. |
| InternalError.GetStreamInfoError | Failed to get stream information. |
| InternalError.GetUpstreamInfoError | Error getting live stream source information. |
| InternalError.NotPermmitOperat | No permission to operate. |
| InternalError.StreamStatusError | Exceptional stream status. |
| InternalError.UpdateDataError | Failed to update data. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |


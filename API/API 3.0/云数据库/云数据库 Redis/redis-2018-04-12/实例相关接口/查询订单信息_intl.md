﻿## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API queries order details.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeInstanceDealDetail |
| Version | Yes | String | Common parameter; the version this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DealIds.N | Yes | Array of String | Array of order IDs |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DealDetails | Array of [TradeDealDetail](/document/api/239/20022#TradeDealDetail) | Order details |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceDealDetail
&DealIds.0=6959052
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "DealDetails": [
      {
        "DealId": "6959052",
        "DealName": "20181101110365",
        "ZoneId": 100002,
        "GoodsNum": 1,
        "Creater": "1817983094",
        "CreatTime": "2018-11-01 21:12:05",
        "OverdueTime": "2018-11-16 21:12:05",
        "EndTime": "2018-11-01 21:13:18",
        "Status": 4,
        "Description": "Successfully shipped",
        "Price": 91949,
        "InstanceIds": [
          "crs-bz8prb7x"
        ]
      }
    ],
    "RequestId": "5d739ed7-af13-489f-b005-aaa57aeaf022"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceDealDetail)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |

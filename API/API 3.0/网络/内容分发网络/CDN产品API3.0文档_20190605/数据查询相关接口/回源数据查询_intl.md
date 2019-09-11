﻿## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

DescribeOriginData describes CDN real-time origin-pull monitoring metrics:

+ Origin-pull traffic (in bytes)
+ Origin-pull bandwidth (in bps)
+ Number of origin-pull requests
+ Number of failed origin-pull requests
+ Origin-pull failure rate (in % with two decimal digits)
+ Aggregated list of 2xx origin-pull status codes and the details of origin-pull status codes starting with 2 (in entries)
+ Aggregated list of 3xx origin-pull status codes and the details of origin-pull status codes starting with 3 (in entries)
+ Aggregated list of 4xx origin-pull status codes and the details of origin-pull status codes starting with 4 (in entries)
+ Aggregated list of 5xx origin-pull status codes and the details of origin-pull status codes starting with 5 (in entries)

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the name of this API: DescribeOriginData |
| Version | Yes | String | Common parameter, the version of this API: 2018-06-06 |
| Region | No | String | Common parameter; optional for this API. |
| StartTime | Yes | Timestamp | Query start time, such as 2018-09-04 10:40:00; the returned result is later than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query start time is 2018-09-04 10:40:00 and the query time granularity is 1 hour, the time for the first returned entry is 2018-09-04 10:00:00 <br/>The gap between the start time and end time should be less than or equal to 90 days |
| EndTime | Yes | Timestamp | Query end time, such as 2018-09-04 10:40:00; the returned result is earlier than or equal to the specified time <br/>According to the specified time granularity, forward rounding is applied; for example, if the query end time is 2018-09-04 10:40:00 and the query time granularity is 1 hour, the time for the last returned entry is 2018-09-04 10:00:00 <br/>The gap between the start time and end time should be less than or equal to 90 days |
| Metric | Yes | String | Specify the query metric, which can be: <br/>flux: Origin-pull traffic (in bytes)<br/>bandwidth: Origin-pull bandwidth (in bps) <br/>request: Number of origin-pull requests <br/>failRequest: Number of failed origin-pull requests <br/>failRate: Origin-pull failure rate (in %) <br/>statusCode: Origin-pull status code; return the aggregated data for 2xx, 3xx, 4xx, and 5xx origin-pull status codes <br/>2xx: Return the aggregated list of 2xx origin-pull status codes and the data for origin-pull status codes starting with 2 (in entries) <br/>3xx: Return the aggregated list of 3xx origin-pull status codes and the data for origin-pull status codes starting with 3 (in entries) <br/>4xx: Return the aggregated list of 4xx origin-pull status codes and the data for origin-pull status codes starting with 4 (in entries) <br/>5xx: Return the aggregated list of 5xx origin-pull status codes and the data for origin-pull status codes starting with 5 (in entries) <br/>It supports the query of a specific status code; the return is empty if the status code has not been generated |
| Domains.N | No | Array of String | Specify the list of domain names to be queried; up to 30 domain names can be queried at a time |
| Project | No | Integer | Specify the project ID to be queried, and you can [view project IDs](https://console.cloud.tencent.com/project) <br/>Please note that if domain names are specified, this parameter will be ignored |
| Interval | No | String | Time granularity: 1-minute; time interval: last 24 hours (inclusive); you see a data point for every minute in last 24 hours <br/>Time granularity: 5-minute; time interval: last 31 days (inclusive); you see a data point for every 5 minutes in last 31 days <br/>Time granularity: 1-hour; time interval: last 31 days (inclusive), and it can return the details for the 1-hour granularity <br/>Time granularity: 1-day; time interval: last 31 days (inclusive); you see a data point for every 5 minutes in last 31 days |
| Detail | No | Boolean | When multiple Domains are specified, the default value is False, which means that the aggregated data for multiple domain names displays <br/>You can set the value to True as needed to return the data for individual Domain (the statusCode metric is currently not supported) |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Interval | String | Data granularity: <br/>min: 1-minute <br/>5min: 5-minute <br/>hour: 1-hour <br/>day: 1-day |
| Data | Array of [ResourceOriginData](/document/api/228/30987#ResourceOriginData) | Origin-pull data details of each resource |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying CDN Origin-Pull Data

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=DescribeOriginData
&StartTime=2018-09-04 00:00:00
&EndTime=2018-09-04 12:00:00
&Metric=flux
&Domains.0=www.test.com
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "123",
    "Data": [
      {
        "Resource": "www.test.com",
        "OriginData": [
          {
            "Metric": "flux",
            "DetailData": [
              {
                "Time": "2018-09-03 00:00:00",
                "Value": 10
              },
              {
                "Time": "2018-09-03 00:05:00",
                "Value": 20
              }
            ],
            "SummarizedData": {
              "Name": "sum",
              "Value": 30
            }
          }
        ]
      }
    ],
    "Interval": 5
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=DescribeOriginData)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CdnDbError | Internal data error. Please submit a ticket for troubleshooting. |
| InternalError.CdnSystemError | System error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnHostInvalidMiddleConfig | Incorrect intermediate server configuration |
| InvalidParameter.CdnHostInvalidParam | Invalid domain name format. Please check and try again. |
| InvalidParameter.CdnInterfaceError | Internal API error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnParamError | Parameter error. Please see the sample parameters in the documentation. |
| InvalidParameter.CdnStatInvalidDate | Invalid date. Please see the sample date in the documentation. |
| InvalidParameter.CdnStatInvalidMetric | Invalid statistical type. Please see the sample statistical analysis in the documentation. |
| InvalidParameter.CdnStatInvalidProjectId | Incorrect project ID. Please check and try again. |
| LimitExceeded.CdnHostOpTooOften | Too frequent operations on domain name. |
| ResourceNotFound.CdnHostNotExists | This domain name does not exist under the account. Please check and try again. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| ResourceNotFound.CdnUserTooManyHosts | The number of accessed domain names exceeds the limit. |
| UnauthorizedOperation.CdnAccountUnauthorized | The sub-account is unauthorized to query full data. |
| UnauthorizedOperation.CdnUserIsSuspended | The CDN service has been suspended. Please restart it and try again. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not on the whitelist, so the operation is prohibited. |

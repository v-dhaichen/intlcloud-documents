## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeSitesVerification) is used to query the verification information of one or more to-be-verified websites.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeSitesVerification |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |
| Urls.N | Yes | Array of String | List of URLs of the website |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of verification information items. |
| SitesVerification | Array of [SitesVerification](/document/api/692/16759#SitesVerification) | List of verification information. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Verification Information List of the Website List

#### Input Example

```
https://cws.tencentcloudapi.com/?Action=DescribeSitesVerification
&Urls.0=http%3A%2F%2Fwww.qcloud.com
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "SitesVerification": [
      {
        "Appid": 1251001047,
        "CreatedAt": "2018-03-19T16:07:57+08:00",
        "Domain": "qq.com",
        "Id": 1,
        "TxtName": "verify-wcpfql",
        "TxtText": "vps9iq4hmn7suiad7v8sn9isawn5yteh",
        "UpdatedAt": "2018-03-23T00:02:11+08:00",
        "ValidTo": "2018-04-18T16:07:57+08:00",
        "VerifyStatus": 1
      }
    ],
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.Malformed | Incorrect data format. |
| InvalidParameter.NotFound | The requested data does not exist. |


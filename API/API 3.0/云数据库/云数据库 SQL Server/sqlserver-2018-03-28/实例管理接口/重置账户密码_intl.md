## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (ResetAccountPassword) resets the password of the specified instance account.

API request rate limit: 20 requests/sec.




## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: ResetAccountPassword |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Database instance ID in the format of mssql-njj2mtpl |
| Accounts.N | Yes | Array of [AccountPassword](/document/api/238/19976#AccountPassword) | Updated account password information array |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| FlowId | Integer | ID of the async task flow for account password change |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Resetting the Account Password of mssql-njj2mtpl

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=ResetAccountPassword
&InstanceId=mssql-njj2mtpl
&Accounts.0.UserName=test_user_4
&Accounts.0.Password=1234qwer()
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "aa77bb20-7522-4b1e-bc0f-ad5d82790b17",
    "FlowId": 30457
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=ResetAccountPassword)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/238/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| ResourceNotFound.AccountNotExist | The account does not exist. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
| ResourceUnavailable.InstanceStatusInvalid | Invalid instance status. |

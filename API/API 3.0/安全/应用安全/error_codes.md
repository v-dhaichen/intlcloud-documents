
## 功能说明

如果返回结果中存在 Error 字段，则表示调用 API 接口失败。例如：

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Error 中的 Code 表示错误码，Message 表示该错误的具体信息。

## 错误码列表

### 公共错误码

| 错误码 | 说明 |
|--------|------|
| AuthFailure.InvalidSecretId | 密钥非法（不是云 API 密钥类型）。 |
| AuthFailure.MFAFailure | MFA 错误。 |
| AuthFailure.SecretIdNotFound | 密钥不存在。 请在控制台检查密钥是否已被删除或者禁用，如状态正常，请检查密钥是否填写正确，注意前后不得有空格。|
| AuthFailure.SignatureExpire | 签名过期。Timestamp 和服务器时间相差不得超过五分钟，请检查本地时间是否和标准时间同步。|
| AuthFailure.SignatureFailure | 签名错误。 签名计算错误，请对照调用方式中的接口鉴权文档检查签名计算过程。|
| AuthFailure.TokenFailure | token 错误。 |
| AuthFailure.UnauthorizedOperation | 请求未 CAM 授权。 |
| DryRunOperation | DryRun 操作，代表请求将会是成功的，只是多传了 DryRun 参数。 |
| FailedOperation | 操作失败。 |
| InternalError | 内部错误。 |
| InvalidAction | 接口不存在。 |
| InvalidParameter | 参数错误。 |
| InvalidParameterValue | 参数取值错误。 |
| LimitExceeded | 超过配额限制。 |
| MissingParameter | 缺少参数错误。 |
| NoSuchVersion | 接口版本不存在。 |
| RequestLimitExceeded | 请求的次数超过了频率限制。 |
| ResourceInUse | 资源被占用。 |
| ResourceInsufficient | 资源不足。 |
| ResourceNotFound | 资源不存在。 |
| ResourceUnavailable | 资源不可用。 |
| UnauthorizedOperation | 未授权操作。 |
| UnknownParameter | 未知参数错误。 |
| UnsupportedOperation | 操作不支持。 |
| UnsupportedProtocol | http(s)请求协议错误，只支持 GET 和 POST 请求。 |
| UnsupportedRegion | 接口不支持所传地域。 |

### 业务错误码

| 错误码 | 说明 |
|:-------|:-----|
| InternalError | 内部错误。 |
| InternalError.ServerError | 服务端无法响应。 |
| InvalidParameter | 参数错误 |
| InvalidParameter.MissingServiceInfo | ServiceInfo结构体参数缺失。 |
| InvalidParameter.PlanIdNotFound | 不能找到指定的加固策略。 |
| InvalidParameterValue.InvalidCoexistItemIdsFilters | 不能同时指定ItemIds和Filters。 |
| InvalidParameterValue.InvalidFilter | 无效的过滤器。 |
| InvalidParameterValue.InvalidItemIds | ItemIds不合法。 |
| InvalidParameterValue.InvalidLimit | Limit不是有效的数字。 |
| InvalidParameterValue.InvalidOffset | Offset不是有效的数字。 |
| InvalidParameterValue.InvalidOrderDirection | OrderDirection参数。 |
| InvalidParameterValue.InvalidOrderField | OrderField取值不合法。 |
| LimitExceeded | 超过配额限制 |
| MissingParameter.MissingAppInfo | AppInfo结构体参数缺失。 |
| MissingParameter.MissingItemId | 缺少ItemId字段。 |
| MissingParameter.MissingItemIds | 缺少ItemIds字段。 |
| ResourceNotFound.ItemIdNotFound | ItemId不存在。 |
| ResourceNotFound.PlanIdNotFound | 无法找到指定的加固策略。 |
| ResourceUnavailable | 资源不可用。 |
| ResourceUnavailable.NotBind | 资源未绑定应用包名。 |
| ResourceUnavailable.NotFound | 找不到该资源。 |
| UnauthorizedOperation | 未授权操作 |
| UnauthorizedOperation.NotWhiteUser | 不是白名单用户。 |

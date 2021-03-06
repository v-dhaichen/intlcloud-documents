## 功能说明
本接口适用于批量将 App 自有帐号导入即时通信 IM，即在即时通信 IM 中为 App 自有帐号创建对应的内部 ID，使未登录过即时通信 IM 的 App 自有帐号能够使用即时通信 IM 服务。
例如，App 开发者通过 REST API 给用户 A 发送一条消息，用户 A 如果没有登录过即时通信 IM 服务，由于腾讯内部没有用户 A 对应的内部 ID，那么给用户 A 发送消息将会失败。需要把用户 A 的帐号导入即时通信 IM，系统为用户 A 创建一个内部 ID，才能通过 REST API 给用户 A 发送消息。

>本接口单次最多支持导入100个帐号，同一个帐号重复导入仅会创建1个内部 ID。

## 接口调用说明
### 请求 URL 示例
```
https://console.tim.qq.com/v4/im_open_login_svc/multiaccount_import?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### 请求参数说明

 下表仅列出调用本接口时涉及修改的参数及其说明，更多参数详情请参考 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| v4/im_open_login_svc/multiaccount_import | 请求接口                             |
| sdkappid           | 创建应用时即时通信 IM 控制台分配的 SDKAppID |
| identifier         | 必须为 App 管理员帐号，更多详情请参见 [App 管理员](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98)                |
| usersig            | App 管理员帐号生成的签名，具体操作请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)    |
| random             | 请输入随机的32位无符号整数，取值范围0 - 4294967295                 |


### 最高调用频率
200次/秒。
### 请求包示例
```
{
"Accounts":["test1","test2","test3","test4","test5"]
}
```

### 请求包字段说明

| 字段 | 类型 | 属性 |说明 |
|---------|---------|---------|-------|
| Accounts | Array|必填 |用户名，单个用户名长度不超过32字节，单次最多导入100个用户名 |

### 应答包体示例

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": "",
    "FailAccounts": [
        "test3",
        "test4"
    ]
}
```

### 应答包字段说明

| 字段  | 类型 | 说明 |
|---------|---------|---------|
| ActionStatus | String | 请求处理的结果，OK 表示处理成功，FAIL 表示失败 |
| ErrorCode|	Integer	|错误码，0表示成功，非0表示失败 |
| ErrorInfo | String | 错误信息 |
| FailAccounts | Array | 导入失败的帐号列表 |

## 错误码说明
除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200。真正的错误码，错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的。
公共错误码（60000到79999）参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 | 含义说明 |
| ------------ | ------------ |
| 70169 | 	服务端内部超时，请稍后重试 |
| 70202  | 服务端内部超时，请稍后重试                          |
| 70398 | 帐号数超限，如需创建多于100个帐号，请将应用升级为专业版，具体操作指引请参见 [购买指引](https://intl.cloud.tencent.com/document/product/1047/34351) |
| 70402 | 参数非法，请检查必填字段是否填充，或者字段的填充是否满足协议要求 |
| 70403 | 请求失败，需要 App 管理员权限 |
| 70500 | 服务器内部错误，请稍后重试|

## 接口调试工具
通过 [REST API 在线调试](https://avc.qcloud.com/im/APITester/APITester.html#v4/im_open_login_svc/multiaccount_import) 工具调试本接口。

## 参考

- 单个帐号导入（[v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953)）
- 帐号删除（[v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955)）
- 帐号检查（[v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956)）
- 失效帐号登录态（[v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957)）

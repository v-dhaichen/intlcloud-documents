## 功能说明
 App 管理员可以通过该接口在群组中发送系统通知。

## 接口调用说明
### 适用的群组类型

|群组类型|支持此 REST API|
|-----------|------------|
|私有群（Private）|是（可指定成员）|
|公开群（Public）|是（可指定成员）|
|聊天室（ChatRoom）|是（可指定成员）|
|音视频聊天室（AVChatRoom）|是（全员）|
|在线成员广播大群（BChatRoom）|是（全员）|

即时通信 IM 内置以上五种群组类型，详情请参阅 [群组系统](https://intl.cloud.tencent.com/document/product/1047/33529)。

>私有群、公开群、聊天室支持向群组中的一部分指定成员发送系统通知，而音视频聊天室和在线成员广播大群只支持向群组中所有成员发送系统通知。

### 请求 URL 示例
```
https://console.tim.qq.com/v4/group_open_http_svc/send_group_system_notification?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### 请求参数说明

下表仅列出调用本接口时涉及修改的参数及其说明，更多参数详情请参考 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| v4/group_open_http_svc/send_group_system_notification | 请求接口                             |
| sdkappid           | 创建应用时即时通信 IM 控制台分配的 SDKAppID |
| identifier         | 必须为 App 管理员帐号，更多详情请参见 [App 管理员](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98)                |
| usersig            | App 管理员帐号生成的签名，具体操作请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)    |
| random             | 请输入随机的32位无符号整数，取值范围0 - 4294967295                 |

### 最高调用频率

200次/秒。

### 请求包示例

- **基础形式**
用来向群中的所有群成员下发系统消息。
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Content": "Hello World" // 系统通知内容
}
```

- **指定接收群成员**
用来向群中的指定的群成员下发系统消息，接收者在 ToMembers_Account 中设置（音视频聊天室不支持指定接收群成员）。
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "ToMembers_Account": [ // 接收者群成员列表，不填或为空表示全员下发
        "peter",
        "leckie"
    ],
    "Content": "Hello World" // 系统通知内容
}
```

### 请求包字段说明

| 字段 | 类型 | 属性 | 说明 |
|---------|---------|---------|---------|
| GroupId | String | 必填 |向哪个群组发送系统通知 |
| ToMembers_Account | Array | 选填 |接收者群成员列表，请填写接收者 UserID，不填或为空表示全员下发  |
| Content | String | 必填 |系统通知的内容  |

### 应答包体示例

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### 应答包字段说明

| 字段 | 类型 | 说明 |
|---------|---------|---------|
| ActionStatus | String | 请求处理的结果，OK 表示处理成功，FAIL 表示失败 |
| ErrorCode|	Integer	|错误码，0表示成功，非0表示失败 |
| ErrorInfo | String | 错误信息  |

## 错误码说明

除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200。真正的错误码，错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的。
公共错误码（60000到79999）参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| 10002  | 服务器内部错误，请重试                                       |
| 10003  | 请求命令字非法                                               |
| 10004  | 参数非法，请根据错误描述检查请求是否正确                     |
| 10007  | 操作权限不足，例如 Public 群组中普通成员尝试执行踢人操作，但只有 App 管理员才有权限 |
| 10010  | 群组不存在，或者曾经存在过，但是目前已经被解散               |
| 10015  | 群组 ID 非法，请检查群组 ID 是否填写正确                     |

## 接口调试工具
通过 [REST API 在线调试工具](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/group_open_http_svc/send_group_system_notification) 调试本接口。

## 参考
在群组中发送普通消息（[v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959)）

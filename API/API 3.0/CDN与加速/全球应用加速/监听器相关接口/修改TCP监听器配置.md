## 1. 接口描述

接口请求域名： gaap.tencentcloudapi.com 。

本接口（ModifyTCPListenerAttribute）用于修改通道实例下TCP监听器配置，包括健康检查的配置，调度策略。

默认接口请求频率限制：20次/秒。

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/608/36935)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：ModifyTCPListenerAttribute |
| Version | 是 | String | 公共参数，本接口取值：2018-05-29 |
| Region | 否 | String | 公共参数，本接口不需要传递此参数。 |
| ListenerId | 是 | String | 监听器ID |
| GroupId | 否 | String | 通道组ID，ProxyId和GroupId必须设置一个，但不能同时设置。 |
| ProxyId | 否 | String | 通道ID，ProxyId和GroupId必须设置一个，但不能同时设置。 |
| ListenerName | 否 | String | 监听器名称 |
| Scheduler | 否 | String | 监听器源站调度策略，支持轮询（rr），加权轮询（wrr），最小连接数（lc）。 |
| DelayLoop | 否 | Integer | 源站健康检查时间间隔，单位：秒。时间间隔取值在[5，300]之间。 |
| ConnectTimeout | 否 | Integer | 源站健康检查响应超时时间，单位：秒。超时时间取值在[2，60]之间。超时时间应小于健康检查时间间隔DelayLoop。 |
| HealthCheck | 否 | Integer | 是否开启健康检查，1开启，0关闭。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 修改TCP监听器配置

修改TCP监听器配置

#### 输入示例

```
https://gaap.tencentcloudapi.com/?Action=ModifyTCPListenerAttribute
&ProxyId=link-bjkpdum1
&ListenerId=listener-o0f3at99
&ListenerName=test10
&Scheduler=rr
&DelayLoop=30
&ConnectTimeout=20
&HealthCheck=1
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "3919ba30-85c4-4cb4-81bf-ff243b50f3dc"
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gaap&Version=2018-05-29&Action=ModifyTCPListenerAttribute)

### SDK

云 API 3.0 提供了配套的开发工具集（SDK），支持多种编程语言，能更方便的调用 API。

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### 命令行工具

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 错误码

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/608/36938#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| FailedOperation | 操作失败 |
| FailedOperation.GroupStatusNotInRuning | 通道组状态为非运行状态，无法操作。 |
| FailedOperation.InstanceStatusNotInRuning | 通道状态为非运行状态，无法操作。 |
| FailedOperation.ListenerHasTask | 监听器正在操作中，请勿重复操作。 |
| FailedOperation.ListenerStatusError | 监听器当前状态无法支持该操作。 |
| InternalError | 内部错误 |
| InvalidParameter | 参数错误 |
| InvalidParameterValue | 参数取值错误 |
| MissingParameter | 缺少参数错误 |
| ResourceNotFound | 资源不存在 |
| UnauthorizedOperation | 未授权操作 |

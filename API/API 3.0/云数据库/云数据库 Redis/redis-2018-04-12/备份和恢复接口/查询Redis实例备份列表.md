## 1. 接口描述

接口请求域名： redis.tencentcloudapi.com 。

查询 CRS 实例备份列表

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：redis.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/239/20005)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeInstanceBackups |
| Version | 是 | String | 公共参数，本接口取值：2018-04-12 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| InstanceId | 是 | String | 待操作的实例ID，可通过 DescribeInstance 接口返回值中的 InstanceId 获取。 |
| Limit | 否 | Integer | 实例列表大小，默认大小20 |
| Offset | 否 | Integer | 偏移量，取Limit整数倍 |
| BeginTime | 否 | String | 开始时间，格式如：2017-02-08 16:46:34。查询实例在 [beginTime, endTime] 时间段内开始备份的备份列表。 |
| EndTime | 否 | String | 结束时间，格式如：2017-02-08 19:09:26。查询实例在 [beginTime, endTime] 时间段内开始备份的备份列表。 |
| Status.N | 否 | Array of Integer | 1：备份在流程中，2：备份正常，3：备份转RDB文件处理中，4：已完成RDB转换，-1：备份已过期，-2：备份已删除。 |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 备份总数|
| BackupSet | Array of [RedisBackupSet](/document/api/239/20022#RedisBackupSet) | 实例的备份数组|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 请求示例

#### 输入示例

```
https://redis.tencentcloudapi.com/?Action=DescribeInstanceBackups
&Limit=5&Offset=0
&InstanceId=crs-5a4py64p
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "RequestId": "2d4387ee-2011-449e-a32b-87f9366f3ef4",
    "TotalCount": 2,
    "RedisBackupSet": [
      {
        "StartTime": "2018-09-04 12:51:21",
        "BackupId": "2e4127f8-affe-11e8-941e-4846fb00c75d",
        "BackupType": "0",
        "Status": 2,
        "Remark": "测试使用",
        "Locked": 0
      },
      {
        "StartTime": "2018-09-04 12:53:06",
        "BackupId": "6cbbf53a-affe-11e8-905b-4846fb00c75d",
        "BackupType": "0",
        "Status": 2,
        "Remark": "xxx",
        "Locked": 0
      }
    ]
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstanceBackups)

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

以下仅列出了接口业务逻辑相关的错误码，其他错误码详见 [公共错误码](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)。

| 错误码 | 描述 |
|---------|---------|
| InternalError.InternalError | 内部错误。 |
| InvalidParameter.InvalidParameter | 业务参数错误。 |
| ResourceNotFound.InstanceNotExists | 根据 serialId 没有找到对应 redis。 |
| UnauthorizedOperation.NoCAMAuthed | 无cam 权限。 |

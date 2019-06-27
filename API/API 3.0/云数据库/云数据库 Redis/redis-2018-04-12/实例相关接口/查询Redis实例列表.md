## 1. 接口描述

接口请求域名： redis.tencentcloudapi.com 。

查询Redis实例列表

默认接口请求频率限制：20次/秒。

注意：本接口支持金融区地域。由于金融区和非金融区是隔离不互通的，因此当公共参数 Region 为金融区地域（例如 ap-shanghai-fsi）时，需要同时指定带金融区地域的域名，最好和 Region 的地域保持一致，例如：redis.ap-shanghai-fsi.tencentcloudapi.com。



## 2. 输入参数

以下请求参数列表仅列出了接口请求参数和部分公共参数，完整公共参数列表见 [公共请求参数](/document/api/239/20005)。

| 参数名称 | 必选 | 类型 | 描述 |
|---------|---------|---------|---------|
| Action | 是 | String | 公共参数，本接口取值：DescribeInstances |
| Version | 是 | String | 公共参数，本接口取值：2018-04-12 |
| Region | 是 | String | 公共参数，详见产品支持的 [地域列表](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)。 |
| Limit | 否 | Integer | 实例列表的大小，参数默认值20 |
| Offset | 否 | Integer | 偏移量，取Limit整数倍 |
| InstanceId | 否 | String | 实例Id，如：crs-6ubhgouj |
| OrderBy | 否 | String | 枚举范围： projectId,createtime,instancename,type,curDeadline |
| OrderType | 否 | Integer | 1倒序，0顺序，默认倒序 |
| VpcIds.N | 否 | Array of String | 私有网络ID数组，数组下标从0开始，如果不传则默认选择基础网络，如：47525 |
| SubnetIds.N | 否 | Array of String | 子网ID数组，数组下标从0开始，如：56854 |
| ProjectIds.N | 否 | Array of Integer | 项目ID 组成的数组，数组下标从0开始 |
| SearchKey | 否 | String | 查找实例的ID。 |
| InstanceName | 否 | String | 实例名称 |
| UniqVpcIds.N | 否 | Array of String | 私有网络ID数组，数组下标从0开始，如果不传则默认选择基础网络，如：vpc-sad23jfdfk |
| UniqSubnetIds.N | 否 | Array of String | 子网ID数组，数组下标从0开始，如：subnet-fdj24n34j2 |
| RegionIds.N | 否 | Array of Integer | 地域ID，已经弃用，可通过公共参数Region查询对应地域 |
| Status.N | 否 | Array of Integer | 实例状态：0-待初始化，1-流程中，2-运行中，-2-已隔离，-3-待删除 |
| TypeVersion | 否 | Integer | 类型版本：1-单机版,2-主从版,3-集群版 |
| EngineName | 否 | String | 引擎信息：Redis-2.8，Redis-4.0，CKV |
| AutoRenew.N | 否 | Array of Integer | 续费模式：0 - 默认状态（手动续费）；1 - 自动续费；2 - 明确不自动续费 |
| BillingMode | 否 | String | 计费模式：postpaid-按量计费；prepaid-包年包月 |
| Type | 否 | Integer | 实例类型：1-Redis老集群版；2-Redis 2.8主从版；3-CKV主从版；4-CKV集群版；5-Redis 2.8单机版；7-Redis 4.0集群版 |
| SearchKeys.N | 否 | Array of String | 搜索关键词：支持实例Id、实例名称、完整IP |

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| TotalCount | Integer | 实例数|
| InstanceSet | Array of [InstanceSet](/document/api/239/20022#InstanceSet) | 实例详细信息列表|
| RequestId | String | 唯一请求 ID，每次请求都会返回。定位问题时需要提供该次请求的 RequestId。|

## 4. 示例

### 示例1 请求示例

#### 输入示例

```
https://redis.tencentcloudapi.com/?Action=DescribeInstances
&Offset=0&Limit=1
&<公共请求参数>
```

#### 输出示例

```
{
  "Response": {
    "InstanceSet": [
      {
        "Appid": 1251006373,
        "AutoRenewFlag": 0,
        "BillingMode": 0,
        "CloseTime": "0000-00-00 00:00:00",
        "Createtime": "0000-00-00 00:00:00",
        "DeadlineTime": "0000-00-00 00:00:00",
        "Engine": "社区版Redis",
        "InstanceId": "crs-7ponppu3",
        "InstanceName": "crs-7ponppu3",
        "InstanceNode": [],
        "InstanceTags": [
          {
            "TagKey": "aaa",
            "TagValue": "111"
          }
        ],
        "InstanceTitle": "实例运行中",
        "OfflineTime": "",
        "Port": 6379,
        "PriceId": 13380,
        "ProductType": "Redis4.0集群版",
        "ProjectId": 0,
        "RedisReplicasNum": 1,
        "RedisShardNum": 3,
        "RedisShardSize": 1024,
        "RegionId": 1,
        "Size": 3072,
        "SizeUsed": 0,
        "SlaveReadWeight": 0,
        "Status": 2,
        "SubStatus": 19,
        "SubnetId": 0,
        "Tags": [],
        "Type": 7,
        "UniqSubnetId": "",
        "UniqVpcId": "",
        "VpcId": 0,
        "WanIp": "10.66.153.160",
        "ZoneId": 100002
      }
    ],
    "RequestId": "e3d683fc-f2ff-43c9-980d-fae7a1166abc",
    "TotalCount": 1
  }
}
```


## 5. 开发者资源

### API Explorer

**该工具提供了在线调用、签名验证、SDK 代码生成和快速检索接口等能力，能显著降低使用云 API 的难度，推荐使用。**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeInstances)

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
| InternalError.DbOperationFailed | 统的 DB 操作错误，可以是 update insert select..。 |
| InvalidParameter | 参数错误 |
| InvalidParameter.EmptyParam | 参数为空。 |
| InvalidParameter.InvalidParameter | 业务参数错误。 |
| InvalidParameter.PermissionDenied | 接口没有cam权限。 |
| UnauthorizedOperation.NoCAMAuthed | 无cam 权限。 |

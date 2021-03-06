﻿## 1. 接口描述

接口：GetMonitorData

接口请求域名： monitor.tencentcloudapi.com

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云数据库REDIS监控数据，入参取值如下：

&Namespace=QCE/REDIS

&Instances.N.Dimensions.0.Name=instanceid

&Instances.N.Dimensions.0.Value为实例的id


## 2. 输入参数


以下请求参数列表仅列出了接口请求参数和部分公共参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478)页面。

### 2.1输入参数
#### 2.1.1 输入参数总览
| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的[地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间，API 3.0接口版本的必须是大写，如： QCE/REDIS |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 endTime不能小于startTime |

#### 2.1.2 各维度对应参数总览

| 参数名称 | 维度名称 | 维度解释 | 格式 |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| Instances.N.Dimensions.0.Name | instanceid | 实例的id | String类型维度名称：instanceid |
| Instances.N.Dimensions.0.Value | instanceid | 具体实例的id | 输入实例的具体redis实例id，如tdsql-123456 也即是实例串号，如crs-ifmymj41，可通过[查询CRS实例列表接口](https://intl.cloud.tencent.com/document/api/239/1384)查询 |
| Instances.N.Dimensions.1.Name | clusterid | 分片的id | String类型维度名称：clusterid ，如果拉取总信息，不传此值，如拉取分片信息，入参必现是clusterid|
| Instances.N.Dimensions.1.Value | clusterid | 具体分片的id | 分片id，通过命令cluster nodes等获取，如tdsql-123456 |


### 2.2 指标名称

每个指标对应的统计粒度（Period）及维度 (dimension) 可取值不一定相同，可通过[DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882)接口获取每个指标支持的统计粒度及维度信息。

#### 2.2.1 实例总信息指标名称
| 指标名称 | 含义 | 单位 |
| --------------------- | ------------ | ---- |
| CmdstatGetMin | get命令数 | 次/分钟 |
| CmdstatGetbitMin | getbit命令数 | 次/分钟 |
| CmdstatGetrangeMin | getrange命令数 | 次/秒 |
| CmdstatHgetMin | hget命令数 | 次/分钟 |
| CmdstatHgetallMin | hgetall命令数 | 次/分钟 |
| CmdstatHmgetMin | hmget命令数 | 次/分钟 |
| CmdstatHmsetMin | hmset命令数 | 次/分钟 |
| CmdstatHsetMin | hset命令数 | 次/分钟 |
| CmdstatHsetnxMin | hsetnx命令数 | 次/分钟 |
| CmdstatLsetMin | lset命令数 | 次/分钟 |
| CmdstatMgetMin | mget命令数 | 次/分钟 |
| CmdstatMsetMin | mset命令数 | 次/分钟 |
| CmdstatMsetnxMin | msetnx命令数 | 次/分钟 |
| CmdstatSetMin | set命令数 | 次/分钟 |
| CmdstatSetbitMin | setbit命令数 | 次/分钟 |
| CmdstatSetexMin | setex命令数 | 次/分钟 |
| CmdstatSetnxMin | setnx命令数 | 次/分钟 |
| CmdstatSetrangeMin | setrange命令数 | 次/分钟 |
| QpsMin | 每秒执行命令数 | 次/分钟 |
| ConnectionsMin | 连接数 | 个 |
| CpuUsMin | cpu利用率 | % |
| InFlowMin | 内网入流量 | Mb/分钟 |
| KeysMin | key总数 | 个 |
| OutFlowMin | 内网出流量 | Mb/分钟 |
| StatGetMin | 所有get命令数 | 次/分钟 |
| StatSetMin | 所有set命令数 | 次/分钟 |
| StorageMin | 已使用容量 | MB/分钟 |
| StorageUsMin | 容量使用率 | % |

#### 2.2.1 实例分片信息指标名称
| 指标名称 | 含义 | 单位 |
| --------------------- | ------------ | ---- |
| CmdstatGetNodeMin | get命令数 | 次/分钟 |
| CmdstatGetbitNodeMin | getbit命令数 | 次/分钟 |
| CmdstatGetrangeNodeMin | getrange命令数 | 次/分钟 |
| CmdstatHgetNodeMin | hget命令数 | 次/分钟 |
| CmdstatHgetallNodeMin | hgetall命令数 | 次/分钟 |
| CmdstatHmgetNodeMin | hmget命令数 | 次/分钟 |
| CmdstatHmsetNodeMin | hmset命令数 | 次/分钟 |
| CmdstatHsetNodeMin | hset命令数 | 次/分钟 |
| CmdstatHsetnxNodeMin | hsetnx命令数 | 次/分钟 |
| CmdstatLsetNodeMin | lset命令数 | 次/分钟 |
| CmdstatMgetNodeMin | mget命令数 | 次/分钟 |
| CmdstatMsetNodeMin | mset命令数 | 次/分钟 |
| CmdstatMsetnxNodeMin | msetnx命令数 | 次/分钟 |
| CmdstatSetNodeMin | set命令数 | 次/分钟 |
| CmdstatSetbitNodeMin | setbit命令数 | 次/分钟 |
| CmdstatSetexNodeMin | setex命令数 | 次/分钟 |
| CmdstatSetnxNodeMin | setnx命令数 | 次/分钟 |
| CmdstatSetrangeNodeMin | setrange命令数 | 次/分钟 |
| QpsNodeMin | 每秒执行命令数 | 次/分钟 |
| ConnectionsNodeMin | 连接数 | 个 |
| CpuUsNodeMin | cpu利用率 | % |
| InFlowNodeMin | 内网入流量 | Mb/分钟 |
| KeysNodeMin | key总数 | 个 |
| OutFlowNodeMin | 内网出流量 | Mb/分钟 |
| StatGetNodeMin | 所有get命令数 | 次/分钟 |
| StatSetNodeMin | 所有set命令数 | 次/分钟 |
| StorageNodeMin | 已使用容量 | Mb/分钟 |
| StorageUsNodeMin | 容量使用率 | % |


## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId。 |

## 4. 错误码表

| 错误代码 | 错误描述 | 英文描述 |
| ---- | ------- | ------------------------------------ |
| -502 | 资源不存在 | OperationDenied.SourceNotExists |
| -503 | 请求参数有误 | InvalidParameter |
| -505 | 参数缺失 | InvalidParameter.MissingParameter |
| -507 | 超出限制 | OperationDenied.ExceedLimit |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败 | InternalError.DBoperationFail |

## 5. 示例

### 示例1 拉取单个云数据库REDIS的get命令数监控数据示例
拉取某个云数据库REDIS某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&[<公共请求参数>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-miv64oan"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```
### 示例2 拉取多个云数据库REDIS的数据get命令数监控数据示例
拉取多个云数据库REDIS某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-123456"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
},
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```


### 示例3 拉取单个云数据库REDIS的实例分片信息get命令数监控数据示例
拉取某个云数据库REDIS实例分片信息某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-1234567
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-1234567
&[<公共请求参数>](https://intl.cloud.tencent.com/document/api/248/4478)
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetNodeMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-1234567"
},{
"Name": "clusterid",
"Value": "tdsql-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```
### 示例4 拉取多个云数据库REDIS的实例分片信息数据get命令数监控数据示例
拉取多个云数据库REDIS实例分片信息某段时间内统计周期为60秒的get命令数监控数据

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/REDIS
&MetricName=CmdstatGetNodeMin
&Period=60
&StartTime=2019-06-04T00:35:00+08:00
&EndTime=2019-06-04T00:40:00+08:00
&Instances.0.Dimensions.0.Name=instanceid
&Instances.0.Dimensions.0.Value=crs-123456
&Instances.0.Dimensions.1.Name=clusterid
&Instances.0.Dimensions.1.Value=tdsql-123456
&Instances.1.Dimensions.0.Name=instanceid
&Instances.1.Dimensions.0.Value=crs-1234567
&Instances.1.Dimensions.1.Name=clusterid
&Instances.1.Dimensions.1.Value=tdsql-1234567
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"StartTime": "2019-06-04 00:35:00",
"EndTime": "2019-06-04 00:40:00",
"Period": 60,
"MetricName": "CmdstatGetNodeMin",
"DataPoints": [
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-1234567"
},{
"Name": "clusterid",
"Value": "tdsql-1234567"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
},
{
"Dimensions": [
{
"Name": "instanceid",
"Value": "crs-123456"
},{
"Name": "clusterid",
"Value": "tdsql-123456"
}
],
"Timestamps": [
1559579700,
1559579760,
1559579820,
1559579880,
1559579940,
1559580000
],
"Values": [
0,
0,
0,
0,
0,
0
]
}
],
"RequestId": "4266ad8d-4318-4169-bfd8-9258c31b228e"
}
}
```
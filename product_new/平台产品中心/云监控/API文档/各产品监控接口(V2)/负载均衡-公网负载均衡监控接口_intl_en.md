﻿## 1. API Description

API: GetMonitorData

Domain name for API request: `monitor.tencentcloudapi.com`

Cloud Load Balancer (CLB) is a service that distributes traffic to multiple CVM instances. For more information, please see the CLB overview page.
Currently, CLB supports four namespaces: `QCE/LB_PUBLIC`, `QCE/LB_PRIVATE`, `QCE/LB_RS_PRIVATE`, and `QCE/LOADBALANCE`.


QCE/LB_PUBLIC: namespace for public network CLB, which includes monitoring data in the CLB instance and real server dimensions.

QCE/LB_PRIVATE: namespace for private network CLB, which includes monitoring data in the CLB instance dimension.

QCE/LB_RS_PRIVATE: namespace for private network CLB, which includes monitoring data in the real server dimension. 

QCE/LOADBALANCE: namespace for private network CLB layer-7 data.


API call rate limit: 20 calls/second (1,200 calls/minute). A single request can get the data of up to 10 instances and up to 1,440 data points.

This API may fail due to the rate limit if you need to call a lot of metrics and objects. We recommend spreading call requests across a period of time.

You can use the namespace of public network CLB to query all monitoring data of the public network CLB instance.
Monitoring data can be queried based on the following four combinations of dimensions. The values for input parameters are as follows:

### 1.1. Values of input parameters in public network CLB instance dimension
&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value=IP address


### 1.2. Values of input parameters in public network CLB instance port dimension

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value=IP address

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value=port number

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value=protocol type


### 1.3. Values of input parameters in public network CLB real server dimension

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value=IP address

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value=port number

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value=protocol type

&Instances.N.Dimensions.3.Name= vpcId

&Instances.N.Dimensions.3.Value=VPC ID of CLB instance

&Instances.N.Dimensions.4.Name=lanIp

&Instances.N.Dimensions.4.Value=real server IP of CLB instance




### 1.4. Values of input parameters in public network CLB real server port dimension

&Namespace: QCE/LB_PUBLIC

&Instances.N.Dimensions.0.Name=vip

&Instances.N.Dimensions.0.Value=IP address

&Instances.N.Dimensions.1.Name=loadBalancerPort

&Instances.N.Dimensions.1.Value=port number

&Instances.N.Dimensions.2.Name=protocol

&Instances.N.Dimensions.2.Value=protocol type

&Instances.N.Dimensions.3.Name=vpcId

&Instances.N.Dimensions.3.Value=VPC ID of CLB instance

&Instances.N.Dimensions.4.Name=lanIp

&Instances.N.Dimensions.4.Value=real server IP of CLB instance

&Instances.N.Dimensions.5.Name=port

&Instances.N.Dimensions.5.Value=real server port number of CLB instance


## 2. Input Parameters

The list below contains only the API request parameters and certain common request parameters. Common request parameters need to be added when a call is made. For more information, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/248/4478).

### 2.1. Input parameters

#### 2.1.1. Overview of input parameters

| Parameter Name | Required | Type | Description |
| ----------- | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Action | Yes | String | Common parameter. The value used for this API: GetMonitorData |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-24 |
| Region | No | String | Common parameter, indicating the region of the instance to be queried. For supported regions, please see the [list of regions](https://intl.cloud.tencent.com/document/api/213/15692) supported by CVM |
| Namespace | Yes | String | Namespace. Each Tencent Cloud product has a namespace, such as `QCE/LB_PUBLIC`. This value must be capitalized for API 3.0 |
| MetricName | Yes | String | Metric name. For more information, please see section 2.2 |
| Instances.N | Yes | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | Combination of instance object dimensions |
| Period | No | Integer | Statistical period for monitoring data in seconds. Default value: 300 |
| StartTime | No | Datetime | Start time, such as "2016-01-01 10:25:00". Default value: "00:00:00" on the current day |
| EndTime | No | Timestamp | End time, which is the current time by default. `EndTime` cannot be earlier than `StartTime` |

#### 2.1.2. Overview of parameters in each dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------ | ---------------- | ------------- | ----------------------------- |
| &Instances.N.Dimensions.0.name | vip | CLB instance VIP | String-type dimension name: vip |
| &Instances.N.Dimensions.0.value | vip | CLB instance VIP | Specific IP address, such as 111.111.111.11 |
| &Instances.N.Dimensions.1.name | loadBalancerPort | CLB instance port | String-type dimension name: loadBalancerPort |
| &Instances.N.Dimensions.1.value | loadBalancerPort | CLB instance port | Specific port number, such as 80 |
| &Instances.N.Dimensions.2.name | protocol | Protocol | String-type dimension name: protocol |
| &Instances.N.Dimensions.2.value | protocol | Protocol | String type. Example: http |
| &Instances.N.Dimensions.3.name | vpcId | VPC ID of CLB instance | String-type dimension name: vpcId |
| &Instances.N.Dimensions.3.value | vpcId | VPC ID of CLB instance | Specific VPC ID, such as 1111 |
| &Instances.N.Dimensions.4.name | lanIp | Real server IP of CLB instance | String-type dimension name: lanIp |
| &Instances.N.Dimensions.4.value | lanIp | Real server IP of CLB instance | Specific IP address, such as 111.222.111.22 |
| &Instances.N.Dimensions.5.name | port | Real server port number of CLB instance | String-type dimension name: port |
| &Instances.N.Dimensions.5.value | port | Real server port number of CLB instance | Specific port number, such as 80 |

### 2.2. Metric name

The statistical granularity (`period`) and dimension (`dimension`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/338821) API can be used to get the `period` and `dimension` supported by each metric.

| Metric Name | Description | Unit |
| ---------------- | ----- | ---- |
| Connum | Current connections | - |
| NewConn | New connections | - |
| Intraffic | Inbound traffic | Mbps |
| Outtraffic | Outbound traffic | Mbps |
| Inpkg | Inbound packets | Packets/sec |
| Outpkg | Outbound packets | Packets/sec |

## 3. Output Parameters

| Parameter Name | Type | Description |
| ---------- | --------------------- | ------------------------------------------------------------ |
| MetricName | String | Monitoring metric |
| StartTime | Timestamp | Data point start time |
| EndTime | Timestamp | Data point end time |
| Period | Integer | Statistical period |
| DataPoints | Array of PointsObject | Monitoring data list |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues |

## 4. Error Codes

| Error Code | Error Description | Error Message |
| ---- | ------- | ------------------------------------ |
| -502 | The resource does not exist. | OperationDenied.SourceNotExists |
| -503 | Incorrect request parameter. | InvalidParameter |
| -505 | Missing parameter. | InvalidParameter.MissingParameter |
| -507 | Limit exceeded. | OperationDenied.ExceedLimit |
| -509 | Incorrect combination of dimensions. | InvalidParameter.DimensionGroupError |
| -513 | Database operation failed. | InternalError.DBoperationFail |

## 5. Samples

### Sample 1 
This example shows you how to get the inbound traffic data of one public network CLB instance using a statistical period of 60 seconds for a specified length of time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_PUBLIC
&MetricName=Intraffic
&Period=60
&StartTime=2019-05-20T16:40:00+08:00
&EndTime=2019-05-20T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=loadBalancerPort
&Instances.0.Dimensions.1.Value=8088
&Instances.0.Dimensions.2.Name=protocol
&Instances.0.Dimensions.2.Value=http
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-20 16:40:00",
"EndTime": "2019-05-20 16:45:00",
"Period": 60,
"MetricName": "Intraffic",
"DataPoints": [
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "111.111.111.11"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
}
],
"RequestId": "b3f5d456-643d-404d-8edb-12345678910"
}
}

```

### Sample 2 
This example shows you how to get the inbound traffic data of multiple public network CLB instances using a statistical period of 60 seconds for a specified time.

#### Input sample code

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace= QCE/LB_PUBLIC
&MetricName=Intraffic
&Period=60
&StartTime=2019-05-20T16:40:00+08:00
&EndTime=2019-05-20T16:45:00+08:00
&Instances.0.Dimensions.0.Name=vip
&Instances.0.Dimensions.0.Value=111.111.111.11
&Instances.0.Dimensions.1.Name=loadBalancerPort
&Instances.0.Dimensions.1.Value=8088
&Instances.0.Dimensions.2.Name=protocol
&Instances.0.Dimensions.2.Value=http
&Instances.1.Dimensions.0.Name=vip
&Instances.1.Dimensions.0.Value=222.222.222.2
&Instances.1.Dimensions.1.Name=loadBalancerPort
&Instances.1.Dimensions.1.Value=8088
&Instances.1.Dimensions.2.Name=protocol
&Instances.1.Dimensions.2.Value=http
&<Common request parameters>
```

#### Output sample code

```
{
"Response": {
"StartTime": "2019-05-20 16:40:00",
"EndTime": "2019-05-20 16:45:00",
"Period": 60,
"MetricName": "Intraffic",
"DataPoints": [
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "111.111.111.11"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
},
{
"Dimensions": [
{
"Name": "loadBalancerPort",
"Value": "8088"
},
{
"Name": "protocol",
"Value": "http"
},
{
"Name": "vip",
"Value": "222.222.222.22"
}
],
"Timestamps": [
1558341600,
1558341660,
1558341720,
1558341780,
1558341840,
1558341900
],
"Values": [
12,
34,
23,
45,
31,
24
]
}
],
"RequestId": "b3f5d456-643d-404d-8edb-12345678910"
}
}

```


## 操作场景
实例（Pod）自动扩缩容功能（Horizontal Pod Autoscaler，HPA）可以根据目标实例 CPU 利用率的平均值等指标自动扩展、缩减服务的 Pod 数量。本文介绍如何通过腾讯云容器服务控制台实现 Pod 自动扩缩容。

## 工作原理
HPA 后台组件会每隔30秒向腾讯云云监控拉取容器和 Pod 的监控指标，然后根据当前指标数据、当前副本数和该指标目标值进行计算，计算所得结果作为服务的期望副本数。当期望副本数与当前副本数不一致时，HPA 会触发 Deployment 进行 Pod 副本数量调整，从而达到自动伸缩的目的。
以 CPU 利用率为例，假设当前有2个实例， 平均 CPU 利用率（当前指标数据）为90%，自动伸缩设置的目标 CPU 为60%， 则自动调整实例数量为：90% × 2 / 60% = 3个。
>!如果用户设置了多个弹性伸缩指标，HPA 会依据各个指标，分别计算出目标副本数，取最大值进行扩缩容操作。

## 注意事项
- 当指标类型选择为 **CPU 利用率（占 Request）**时，必须为容器设置 CPU Request。
- 策略指标目标设置合理，例如设置70%给容器和应用，预留30%的余量。
- 保持 Pod 和 Node 健康（避免 Pod 频繁重建）。
- 保证用户请求的负载均衡稳定运行。
- HPA 在计算目标副本数时会有一个10%的波动因子。如果在波动范围内，HPA 并不会调整副本数目。
- 如果服务对应的 Deployment.spec.replicas 值为0，HPA 将不起作用。
- 如果对单个 Deployment 同时绑定多个 HPA ，则创建的 HPA 会同时生效，会造成的集群反复扩缩容。

## 前提条件
- 已 [注册腾讯云账户](https://intl.cloud.tencent.com/register)。
- 已登录 [腾讯云容器服务控制台](https://console.cloud.tencent.com/tke2)。
- 已创建集群。关于创建集群，详情请参见 [创建集群](https://intl.cloud.tencent.com/document/product/457/30637)。



## 操作步骤

### 开启自动扩缩容
可以通过以下三种方式开启自动扩缩容。

#### 通过设置实例数量调节
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 单击需要创建伸缩组的集群 ID，进入工作负载 Deployment 详情页，选择【新建】。如下图所示：
![](https://main.qcloudimg.com/raw/d272088adb54a4723fb2ce6cdfaffb9c.png)
3. 在“新建Workload”页面，设置实例数量为**自动调节**。如下图所示：
![](https://main.qcloudimg.com/raw/8c8da95b1cfd44308b6d40fbb49a75d7.png)
 - **触发策略**：自动伸缩功能依赖的策略指标。详情请参见 [指标类型](#IndicatorType)。
 - **实例范围**：请根据实际需求进行选择，实例数量会在设定的范围内自动调节，不会超出该设定范围。

#### 通过新建自动伸缩组
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 单击需要创建伸缩组的集群 ID，进入工作负载 Deployment 详情页，选择【自动伸缩】。
3. 在“HorizontalPodAutoscaler”页面，单击【新建】。如下图所示：
![](https://main.qcloudimg.com/raw/bda264f5db79392defa3daf4d4bbd633.png)
3. 在“新建Hpa”页面，根据以下提示，进行 HPA 配置。如下图所示：
![](https://main.qcloudimg.com/raw/adae2f7f599460e64bd2a98f10eed7e3.png)
 - **名称**：输入要创建的自动伸缩组的名称。
 - **命名空间**：请根据实际需求进行选择。
 - **关联deployment**：不能为空，请根据实际需求进行选择。
 - **触发策略**：自动伸缩功能依赖的策略指标，详情请参见 [指标类型](#IndicatorType)。
 - **实例范围**：请根据实际需求进行选择，实例数量会在设定的范围内自动调节，不会超出该设定范围。
4. 单击【创建Hpa】，完成 HPA 的创建。

#### 通过 YAML 创建
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 单击需要创建伸缩组的集群 ID，进入工作负载 Deployment 详情页。
3. 单击该页面右上角【YAML创建资源】。如下图所示：
![](https://main.qcloudimg.com/raw/4d5d15673ff9881bc9182f82b1a2fe99.png)
4. 在“YAML创建资源”页面，根据实际需求编辑内容，单击【完成】，即可新建 HPA 。


### 更新自动扩缩容规则
可以通过以下三种方式更新服务自动扩缩容规则。

#### 通过更新实例数量
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 选择需要创建伸缩组的集群 ID，进入工作负载 Deployment 详情页，单击【更新实例数量】。如下图所示：
![](https://main.qcloudimg.com/raw/c7076730276c064596c1baa28bd5b9c2.png)
3. 在“更新实例数量”页面，根据实际需求进行设置，并单击【更新实例数量】。如下图所示：
![](https://main.qcloudimg.com/raw/97f1c95853ae69ef5320eeda23e498ec.png)

#### 通过修改 Hpa 配置
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 选择需要创建伸缩组的集群 ID，进入工作负载 Deployment 详情页，单击【自动伸缩】。
3. 在“HorizontalPodAutoscaler”页面，单击需要更新配置的 HPA 所在行右侧的【修改配置】。如下图所示：
![](https://main.qcloudimg.com/raw/2c67734ce03b4d86fca300944eff4c71.png)
3. 在“更新Hpa配置”页面，根据实际需求进行设置，并单击【更新Hpa】。如下图所示：
![](https://main.qcloudimg.com/raw/ec12fdd858ff29ce7cef3b696465590b.png)

#### 通过编辑 YAML 更新
1. 单击左侧导航栏中【[集群](https://console.cloud.tencent.com/tke2/cluster)】，进入“集群管理”页面。
2. 单击需要创建伸缩组的集群 ID，选择【自动伸缩】。
3. 在“HorizontalPodAutoscaler”页面，选择需要更新配置的 HPA 所在行右侧的【编辑YAML】。如下图所示：
![](https://main.qcloudimg.com/raw/8157b4ae8e2a072d9c3443e66a217b4d.png)
3. 在“更新HorizontalPodAutoscaler”页面，根据实际需求进行编辑，单击【完成】即可。


<span id="IndicatorType"></span>
## 指标类型

### CPU指标
| 指标名 | 单位 | 描述 |
|----------------|---------|------------------------------------------------------|
| CPU 使用量 |  核 | Pod 的 CPU 使用量 |
|CPU 利用率（占节点） |  %  | Pod 的 CPU 使用量占节点总量之比 |
|CPU 利用率（占 Request）| % | Pod 的 CPU 使用量和设置的 Request 值之比 |
|CPU 利用率（占 Limit）|  %  | Pod 的 CPU 使用量和设置的 Limit 值之比 |

### 内存
| 指标名 | 单位 | 描述 |
|----------------|---------|------------------------------------------------------|
| 内存使用量 |  B | Pod 的内存使用量（含缓存） |
| 内存使用量（不包含 Cache） | B | Pod 内所有 Container 的真实内存使用量（不含缓存）|
| 内存利用率（占节点）| %  | Pod 的内存使用量占节点总量之比 |
| 内存利用率（占节点，不包含 Cache）| % |Pod 内所有 Container 的真实内存使用量（不含缓存）占节点总量之比|
| 内存利用率（占 Request） | %  | Pod 的内存使用量和设置的 Request 值之比 |
| 内存利用率（占 Request，不包含Cache）| % | Pod 内所有 Container 的真实内存使用量（不含缓存）和设置的 Request 值之比 |
| 内存利用率（占 Limit） | % | Pod 的内存使用量和设置的 Limit 值之比 |
| 内存利用率（占 Limit，不包含 Cache）| % | Pod 内所有 Container 的真实内存使用量（不含缓存）和设置的 Limit 值之比 |

### 硬盘
| 指标名 | 单位 | 描述 |
|----------------|---------|------------------------------------------------------|
| 硬盘写流量 | KB/s | Pod 的硬盘写速率 |
| 硬盘读流量 | KB/s | Pod 的硬盘读速率 |
| 硬盘读 IOPS | 次/s | Pod 从硬盘读取数据的 IO 次数 |
| 硬盘写 IOPS | 次/s | Pod 把数据写入硬盘的 IO 次数 |

### 网络
| 指标名 | 单位 | 描述 |
|----------------|---------|------------------------------------------------------|
| 网络入带宽 | Mbps | Pod 的入方向带宽之和 |
| 网络出带宽 | Mbps | Pod 的出方向带宽之和 |
| 网络入流量 | KB/s | Pod 的入方向流量之和 |
| 网络出流量 | KB/s | Pod 的出方向流量之和 |
| 网络入包量 | 个/s | Pod 的入方向包数之和 |
| 网络出包量 | 个/s | Pod 的出方向包数之和 |

本文将为您详细介绍 NAT 网关的费用组成和收费标准。
## 计费说明
NAT 网关服务费用包含两部分：网关费用（按小时计费）和访问 Internet 产生的流量费用。
- 网关费用请参见 **计费模式**。
- 流量费用请参见 [云服务器网络费用](https://intl.cloud.tencent.com/document/product/213/10578) 中的按流量计费。

## 计费模式
NAT 网关本体计费模式如下表：

![image-20191111154038098](/Users/chuchuliu/Library/Application Support/typora-user-images/image-20191111154038098.png)

 >**注意：**
 - 当用户账号开通了带宽包共享带宽功能时，NAT 网关产生的出流量按照带宽包整体结算（不再重复收取网络流量费）。建议您限制 NAT 网关的出带宽，以免因 NAT 网关出带宽过高产生高额的带宽包费用，详情请参见 [带宽包计费详情](https://intl.cloud.tencent.com/document/product/213/10578)。
 - 欠费逻辑：与按量计费主机保持一致，详情请参见 [按量计费云服务器欠费说明](https://intl.cloud.tencent.com/document/product/213/2181)。
 - NAT 网关具备双机热备的特性，系统每 3 秒会分别给 NAT 网关的主备服务器发送一个 5 KB 的探测包，因此每天会产生 0.2747 GB 的流量，可能会造成少量费用。

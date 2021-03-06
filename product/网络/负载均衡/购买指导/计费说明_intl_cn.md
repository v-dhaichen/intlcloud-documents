## 计费项说明
内网负载均衡免费，公网负载均衡仅收取实例租用费。公网负载均衡绑定的云服务器必须购买公网网络，网络购买详情参见 [公网计费模式](https://intl.cloud.tencent.com/document/product/213/10578).

## 按量计费说明
公网负载均衡的实例租用费采用按量计费，每一天（24h）结算一次，不需要提前支付整个使用期间的费用。
- 每一天（24h）结算一次；
- 结算时按实际使用天数计价；
- 计费的起点以负载均衡实例创建成功的时间点为准，终点以您发起销毁操作的时间点为准；
- 使用不足一天将按照一天进行扣费。

>!按量计费的负载均衡实例创建时会预先扣除一天的实例费用，请保证您的账户余额足够。
负载均衡购买后，即使处于闲置状态（无访问，未绑定后端主机）也会持续收取每天的实例配置费用。

## 各地域实例费用
公网负载均衡各地域的实例配置费用如下表所示。

|  地域 | 实例费用<br>（美元/天)|
|---------|---------|
| 广州/上海/北京/成都/重庆 | 0.07 |  
| 中国香港/首尔/孟买/曼谷 | 0.21 |
| 东京 | 0.22 |
| 新加坡/法兰克福/多伦多/莫斯科 | 0.14 |
| 硅谷/弗吉尼亚 | 0.12 |

## 欠费隔离策略

- 实例欠费后延时24小时停服，在欠费后24小时内会以短信/邮件的方式提醒用户尽快续费，在欠费后24小时内进行充值，您的服务将不会受到停服影响。
- 实例欠费24小时后，如果用户未完成续费操作，则暂停实例服务，进入**隔离状态**。实例被隔离后将停止服务，用户所占用的负载均衡实例也将停止计费。实例相关配置数据会保留7天。用户在7天内充值补足欠费后，服务会自动开启，可以继续使用。欠费超过7天，将视为用户主动放弃使用负载均衡服务，相关配置数据也会被释放。
- 腾讯云将在隔离状态实例释放前的1天进行短信/邮件提醒，实例被释放后相关配置数据将被永久删除，不可恢复。

>!负载均衡不会主动解除与 CVM 的绑定关系，但当**云服务器**进入隔离状态（按量计费云服务器欠费两小时以上）时，会强制解除与 LB 的绑定关系。

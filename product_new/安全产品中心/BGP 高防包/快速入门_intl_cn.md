BGP 高防包为腾讯云公网 IP 提供更高的 DDoS 防护能力，可支持防护 CVM、CLB、NAT、WAF 等产品和服务。BGP 高防包接入便捷，无需变更业务 IP，可快速完成防护配置。
目前，腾讯云 BGP 高防包提供独享包与共享包两种类型的高防包。
## 前提条件
在绑定防护 IP 前，您需要成功 [购买 BGP 高防包实例](https://intl.cloud.tencent.com/document/product/1029/31748)。

## 操作步骤
1. 登录 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/dayu/bgp_v2)，前往【BGP高防包】>【资产列表】。
• 若您的 BGP 高防包实例是独享包，则选择【独享包】页签。
• 若您的 BGP 高防包实例是共享包，则选择【共享包】页签。
1. 选择目的高防包实例所在地域，单击目的高防包实例所在行的操作项【绑定设备】。
![](https://main.qcloudimg.com/raw/dd16c73f416aa57ca7671effcc49c266.png)
3. 在【绑定设备】页面，根据实际防护需求选择【关联设备类型】与【选择关联机器】。
  - 若您的 BGP 高防包实例是独享包，仅支持绑定一个关联机器。
	 ![](https://main.qcloudimg.com/raw/5bd85e4544a0a7926e90f98961943f63.png)
 - 若您的 BGP 高防包实例是共享包，【关联设备类型】与【选择关联机器】均允许多选，【选择关联机器】数量不得超过 [购买 BGP 高防包实例](https://intl.cloud.tencent.com/document/product/1029/31748) 时设置的【IP 数量】。
 ![](https://main.qcloudimg.com/raw/226b6cb6c2f39a5c53e08e7ea191a387.png)

 >只有账号被添加至白名单的用户才能在控制台进行托管 IP 绑定高防包操作。如有需求，请 [联系我们](https://intl.cloud.tencent.com/support) 进行咨询或 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请加入白名单。
4. 单击【确定】。


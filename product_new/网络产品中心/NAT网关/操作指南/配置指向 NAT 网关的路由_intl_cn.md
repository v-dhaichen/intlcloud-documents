创建 NAT 网关后，需要配置路由规则，将子网流量指向 NAT 网关。
1. 在 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 左侧目录中，单击【路由表】。
2. 在路由表列表中，单击需要访问 Internet 的子网所关联的路由表 ID 进入详情页，在路由策略中单击【新增路由策略】。
3. 在弹框中输入目的端，下一跳类型选择【NAT 网关】，下一跳选择已创建的 NAT 网关 ID。
![2](https://main.qcloudimg.com/raw/8921a0084f243ea6edde02087b8c5651.png)
4. 单击【确定】完成以上配置后，关联此路由表的子网内的云服务器访问 Intenet 的流量将指向 NAT 网关。

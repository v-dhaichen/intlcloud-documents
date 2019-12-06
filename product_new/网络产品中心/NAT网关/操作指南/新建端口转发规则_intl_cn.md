端口转发表是 NAT 网关上的一张配置表，用于配置 NAT 网关上的 DNAT 功能，可将 VPC 内云服务器的 **[ 内网 IP，协议，端口 ]** 映射成 **[ 外网 IP，协议，端口 ]**，使得云服务器上的资源可被外网访问。
下面将为您详细介绍如何新建端口转发规则。
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【私有网络】进入私有网络控制台，在左侧目录中单击【NAT 网关】。
2. 在列表中单击需要修改的 NAT 网关 ID 进入详情页，单击选项卡中的【端口转发】。
 ![1](https://main.qcloudimg.com/raw/0eddd59eb57b91097b08313a5abf96e0.png)
3. 单击【新建】，选择协议、外部 IP 端口及内部 IP 端口后，单击【确定】即可。
 >内部 IP 仅支持该 VPC 内的云服务器内网 IP。
 >
![](https://main.qcloudimg.com/raw/73f23075cf676a7abad3fdf2e190a442.png)

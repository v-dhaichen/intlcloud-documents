By instantly enabling and disabling routing policies, CCN makes it possible to smoothly migrate a peering connection-enabled VPC to CCN.
Scenario description:
VPC1 and VPC2 are interconnected through a peering connection and now need to be joined to CCN to achieve full-mesh interconnection with other VPCs.
IP address range 1: VPC1 in Guangzhou: 192.168.0.0/16, subnet A: 192.168.0.0/24, subnet B: 192.168.1.0/24.
IP address range 2: VPC2 in Shanghai: 10.0.0.0/16, subnet C: 10.0.0.0/24, subnet D: 10.0.1.0/24.
![Image description](https://main.qcloudimg.com/raw/82c21d3fd060fdc8ef10816a31768105.png)
You need to complete the following steps:
1. Create a CCN instance (if there is already one, skip this step). For more information, see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
2. Associate VPC1 and VPC2 with the corresponding CCN instance. For more information, see [Associating a Network Instance](https://intl.cloud.tencent.com/document/product/1003/30064).
3. In the routing table of the CCN instance, you can see the routing policy with the subnets in VPC1 and VPC2 as the destination.
![Image description](https://main.qcloudimg.com/raw/21402428cb47bdd85735f93806363225.png)
4. Enter the routing table of the subnets in VPC1 to check the routing conditions.
5. Enter the routing table of the subnets in VPC2 to check the routing conditions.
Case 1: If the route automatically distributed by CCN has no conflict with the existing peering connection, it is valid by default and you do not need to do anything.
![Image description](https://main.qcloudimg.com/raw/e313d637cef9c71dfb34bf15ec6468c7.png)
Case 2: If the route automatically distributed by CCN has an overlapping conflict with the existing peering connection, you need to first **disable** the routing policy whose next hop is the peering connection and then **enable** the routing policy whose next hop is the CCN.
![Image description](https://main.qcloudimg.com/raw/edacdeaaca0194ca309eb834c496c540.png)
Case 3: If the route automatically distributed by CCN has an inclusive conflict with the existing peering connection, you can **enable** the routing policy whose next hop is the CCN and then set forwarding based on the longest mask match principle. It is recommended that you [disable] the routing policy whose next hop is the peering connection to avoid duplicate billing.
![Image description](https://main.qcloudimg.com/raw/81779321f3799684670fdffdcb9b0731.png)








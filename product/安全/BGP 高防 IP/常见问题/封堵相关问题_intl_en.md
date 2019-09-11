## Why is my Anti-DDoS Advanced IP blocked when it’s being attacked?

Tencent Cloud reduces the cost by sharing infrastructure, with a public IP shared among all users. 
When a massive traffic attack occurs, the entire Tencent cloud network may be affected, in addition to the target servers.  In order to prevent non-targeted servers from being affected and ensure network stability, we need to block the targeted server IP.

## Why isn’t unlimited Anti-DDoS Advanced traffic free?

DDoS attacks have negative effects on not only the targets but also the entire cloud network, affecting other non-targeted users in the cloud as well. Moreover, the cost of building the anti-DDoS system is very high, including the cleaning cost and the bandwidth cost. Specifically, the largest expense is bandwidth and it is calculated based on total traffic - there is no difference between normal traffic and attack traffic in terms of the bandwidth cost. Therefore, although Tencent Cloud can afford limited free DDoS Basic service for all users,  we have to block inbound public network traffic of the targeted servers when attack traffic exceeds the free quota.

## Why can't my IP be recovered immediately after the attack ends?

A DDoS attack usually does not stop immediately after the IP blocking and how long it lasts is uncertain. Tencent Cloud security team set the default blocking period based on big data analysis. Since the IP blocking takes effect in the ISP's network, Tencent Cloud is unable to monitor whether or not the attack traffic flow has been stopped. If the IP is recovered while the attack is still going on, the IP will be blocked again, where there’s a gap between the recovery and the re-blocking that the attack traffic can take advantage of to directly enter the Tencent Cloud's basic network, resulting in negative effects on other cloud users.  In addition, the IP blocking is a service Tencent cloud purchase from ISPs with limited numbers of blocking and blocking frequency. 

## How can I restore the business while my IP is being blocked?

We recommend that you upgrade your service pack to one has the higher defense capacity and configure the original forwarding rules.
If your server is not deployed on Tencent Cloud, we recommend you change the real server IP, [purchase](https://intl.cloud.tencent.com/document/product/297/15483) and use [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/16497) to ensure the normal operation of your business.

## How can I recover the blocked IP earlier in case of an emergency?

You can upgrade the base protection capacity so that the blocked IP can be recovered automatically.

## How do I connect to a blocked server?

There are two ways to connect to a blocked server:

- Connect the blocked server via the private IP through another CVM in the same region;
- Log in to [CVM console](https://console.cloud.tencent.com/cvm), select the blocked CVM and click **Log In**  and connect via browser VNC.

## How can I prevent the IP from being blocked?

When you purchasing Anti-DDoS Advanced, select an appropriate protection bandwidth based on the historical attack traffic data to ensure that the protection bandwidth is higher than the attack traffic peak.

## How can I prevent my anti-DDoS IP from being blocked again?

We recommend you upgrade the base protection bandwidth or elastic protection bandwidth. Elastic protection can help defense against high-traffic attacks, and you only pay for what you use per day, which reduces your cost.

Anti-DDoS Pro provides Tencent Cloud public IP with higher anti-DDoS capability. It supports Tencent Cloud services like CVM, CLB, NAT, and WAF. Accessing Anti-DDoS Pro is convenient. It requires no change of business IP, and allows for fast protection configuration.
Currently, Anti-DDoS Pro provides two types of instances, Single IP instance and the Multi-IP instance.
## Prerequisites
Before you bind the protected IP, you need to successfully [purchase an Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).

## Steps
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and go to **Anti-DDoS Pro** -> **Resource List**.
• For Single IP instances, please select **Single IP Instance** tab.
• For Multi-IP instance, please select **Multi-IP Instance** tab.
1. Select the region of the target Anti-DDoS Pro instance and click **Bind Resource** in the line of the instance.
![](https://main.qcloudimg.com/raw/4fc76e35b8a449cd8a3606b86ca93998.png)
3. On the **Bind Resource** page, select **Associated Resource Type** and **Associated Resource** according to the actual protection demand.
  - One Single IP instance can only be bound with one resource.
	 ![](https://main.qcloudimg.com/raw/a6531effe9b2fa348ed7f67b515039d3.png)
 - For Multi-IP instance, you can select multiple items in **Associated Resource Type** and **Associated Resource**. The number of **Associated Resource** cannot exceed the **IP Number** set when you [purchase the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).
 ![](https://main.qcloudimg.com/raw/3b08e8d8e9dae86401eb3221ec2bbe47.png)

 > Binding hosted IP with Anti-DDoS Pro instance is only available to whitelisted users now. If necessary, please [contact us](https://intl.cloud.tencent.com/support) for consultation, or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
4. Click **OK**.


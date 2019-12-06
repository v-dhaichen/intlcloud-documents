Security groups are configured to manage whether a Cloud Virtual Machine (CVM) can be accessed. You can configure inbound and outbound rules for security groups to specify whether your server can be accessed or can access other network resources.
Default inbound and outbound rules for security groups are as follows:
- **To ensure data security, the inbound rule for a security group is a rejection policy that denies remote access from external networks.** To allow your CVM to be accessed externally, you need to open the inbound rule for the corresponding port to the Internet.
- The outbound rule for a security group specifies whether your CVM can access external network resources. If you select **Open All Ports** or **Open Ports 22, 80, 443, and 3389 and ICMP**, the outbound rule for the security group opens all ports to the Internet. If you select a custom security group rule, the outbound rule blocks all ports by default, and you need to set the outbound rule to allow the corresponding port to access external network resources.

## Common Use Cases
This document introduces several common use cases for security groups. If any of the following cases meets your requirements, you can set your security groups according to the configuration recommended for the corresponding use case.

### Scenario 1: Remotely Connecting to a Linux CVM via SSH
**Case**: You have created a Linux CVM and want to remotely connect to the CVM via SSH.
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), set **Type** to **Linux login** and open TCP port 22 to the Internet to allow Linux login via SSH.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can be remotely connected to via SSH.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Linux login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>TCP: 22</td><td>Allow</td></tr>
</table>

### Scenario 2: Remotely Connecting to a Windows CVM via RDP
**Case**: You have created a Windows CVM and want to remotely connect to the CVM via Remote Desktop Connection (RDP).
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), set **Type** to **Windows login** and open TCP port 3389 to the Internet to enable remote login to Windows.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This enables you to configure the source IP addresses of the CVMs that can be remotely connected to via RDP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Windows login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>TCP: 3389</td><td>Allow</td></tr>
</table>

### Scenario 3: Pinging a CVM on a Public Network
**Case**: You have created a CVM and want to test whether the communication between this CVM and other CVMs is normal.
**Solution**: Test the connection by using the ping program. Specifically, when [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), set **Type** to **Ping** and open Internet Control Message Protocol (ICMP) ports to the Internet to enable other CVMs to gain access to this CVM by using ICMP.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can gain access to this CVM by using ICMP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Ping</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>ICMP</td><td>Allow</td></tr>
</table>

### Scenario 4: Remotely Logging In to a CVM via Telnet
**Case**: You want to remotely log in to a CVM via Telnet.
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), configure the following security group rule:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>TCP: 23</td><td>Allow</td></tr>
</table>

### Scenario 5: Authorizing Access to a Web Service via HTTP or HTTPS
**Case**: You have built a website and want to allow users to access your website via HTTP or HTTPS.
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), configure the following security group rules as required:
- Allow all IP addresses on the public network to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Allow</td></tr>
</table>
- Allow some IP addresses on the public network to access this website.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>The IP address or IP address range that is allowed to access your website</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>The IP address or IP address range that is allowed to access your website</td><td>TCP: 443</td><td>Allow</td></tr>
</table>

### Scenario 6: Allowing an External IP Address to Access a Specified Port
**Case**: You have deployed a service and want the specified service port (such as port 1101) to be externally accessible.
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), set **Type** to **Custom** and open TCP port 1101 to the Internet to allow external access to the specified service port.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows the source IP address to access the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>TCP: 1101</td><td>Allow</td></tr>
</table>

### Scenario 7: Denying Access to a Specified Port from External IP Addresses
**Case**: You have deployed a service and want to prevent external access to a specified service port (such as port 1102).
**Solution**: When [Adding an Inbound Rule](https://intl.cloud.tencent.com/document/product/213/18197), set **Type** to **Custom**, configure TCP port 1102, and set **Policy** to **Reject** to deny external access to the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: Enter your specified IP address or IP address range</li></ul></td><td>TCP: 1102</td><td>Reject</td></tr>
</table>

### Scenario 8: Allowing a CVM to Access Only a Specified External IP Address
**Case**: You want your CVM to access only a specified external IP address.
**Solution**: Add two outbound security group rules by referring to the following configurations:
- Allow the CVM instance to access a specified external IP address
- Disallow the CVM instance to access any public IP addresses via any protocol.

> Rules that permit access have a higher priority than those that deny access.
>
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>The specified public IP address that can be accessed by the CVM</td><td>The required protocol and port</td><td>Allow</td></tr>
<tr><td>Outbound</td><td>Custom</td><td>0.0.0.0/0</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 9: Denying a CVM from Accessing a Specified External IP Address
**Case**: You do not want your CVM to access a specified external IP address.
-**Solution**: Add a security group rule by referring to the following configuration:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>The specified public IP address that you do not want to be accessed by the CVM</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 10: Uploading or Downloading a File to or from a CVM via FTP
**Case**: You want to upload a file to or download a file from a CVM by using an FTP program.
-**Solution**: Add a security group rule by referring to the following configuration:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol and Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td>0.0.0.0/0</td><td>TCP: 20 to 21</td><td>Allow</td></tr>
</table>

## Combination of Multiple Scenarios
In an actual scenario, you may want to configure multiple security group rules based on service requirements; for example, configuring inbound or outbound rules at the same time. One CVM may be bound to one or more security groups. When a CVM is bound to multiple security groups, these security groups are matched and executed in descending order of priorities. You can adjust the priorities of these security groups whenever needed. For more information about the priorities of security group rules, see [Rule Priorities](https://intl.cloud.tencent.com/document/product/213/12452).


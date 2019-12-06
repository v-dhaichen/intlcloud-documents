
This document introduces how to troubleshoot the problem where being unable to remotely log into a Linux or Windows CVM due to high bandwidth usage.

## Fault symptoms
- In [CVM Console](https://console.cloud.tencent.com/cvm/index), the bandwidth monitoring data of the CVM prompts that the bandwidth usage is too high, and it not possible to connect to the CVM.
<!-- - Use [self-diagnose](https://console.cloud.tencent.com/workorder/check) tool and get the result that the outbound bandwidth occupation is too high. -->

## Locating and Troubleshooting the Fault

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. Select the CVM to check and click **Log in**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. In the **Log into Windows/Linux Instance** window that pops up, select **Other login methods (VNC)**, and click **Log in** to log in to the CVM.
4. In the login window that pops up, select **Send Remote Command** in the top left corner, and click **Ctrl-Alt-Delete** to enter the system login interface as shown below:
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### Windows CVMs
After using VNC to log into the Windows CVM, you must execute the following operations:
> The following operations take a CVM with the Windows Server 2012 system as an example.
>
1. In the CVM, click <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>. Select **Task Manager** to open the **Task Manager** window.
2. Select the **Performance** tab page and click **Open Resource Monitor**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/a635da7e769cc1424b225674803e5cb1.png)
3. In the **Resource Monitor** that is open, check which process consumes more bandwidth. According to your actual business, determine whether the process is normal. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/6a131472fc52bb4f5c4d5f57a1b7b010.png)
 - If the process that consumes a lot of bandwidth is a normal business process, please check whether it is due to a change of access volume, and whether you need to optimize the capacity or [upgrade CVM configurations](https://intl.cloud.tencent.com/document/product/213/2178).
 - If the process that consumes a lot of bandwidth is an exceptional process, there may be a virus or a Trojan. You can terminate the process yourself or use security software. You can also back up the data and reinstall the system.
 > In Windows systems, many virus processes are disguised as system processes. You can use process information in **Task Manager** > **Processes** to perform preliminary inspection:
 > Normal system processes have complete signatures and descriptions, and most are located under the C:\Windows\System32 directory. Virus program names may be the same as system processes, but they do not have signatures or descriptions. The location will also be abnormal.
 > 
 - If the process that consumes a lot of bandwidth is a Tencent Cloud component process, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.

### Linux CVMs
After using VNC to log into the Linux CVM, you must execute the following operations:
> The following operations take a CVM with the CentOS 7.6 system as an example.
>
1. Execute the following command to install the iftop tool. The iftop tool is a traffic monitoring gadget for the Linux CVM.
```
yum install iftop -y
```
>For Ubuntu system, execute the `apt-get install iftop -y` command.
>
2. Execute the following command to install lsof.
```
yum install lsof -y
```
3. Execute the following command to run iftop. This is shown in the following figure:
```
iftop
```
![](https://main.qcloudimg.com/raw/7fccea56d998a65df6ff7e9348772910.png)
 - `<=`、`=>` indicates the direction of traffic
 - TX indicates the delivery traffic
 - RX indicates the receiving traffic
 - TOTAL indicates total traffic
 - cum indicates the total traffic from running iftop to the current time
 - peak indicates traffic peaks
 - rates separately indicates the average traffic over the last 2s, 10s, and 40s
4. According to the IP of the consumed traffic in iftop, execute the following command to check the process connected to this IP.
```
lsof -i | grep IP
```
For example, if the IP of the consumed traffic is 201.205.141.123, run the following command:
```
lsof -i | grep 201.205.141.123
```
According to the results returned as follows, we know that the CVM bandwidth is mainly consumed by the SSH process.
```
sshd       12145    root    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
sshd       12179  ubuntu    3u  IPV4  3294018       0t0   TCP 10.144.90.86:ssh->203.205.141.123:58614(ESTABLISHED)
```
5. View the process that consumes bandwidth, and determine whether the process is normal.
 - If the process that consumes a lot of bandwidth is a normal process, please check whether it is due to a change of access volume, and whether you need to [upgrade CVM configurations](https://intl.cloud.tencent.com/document/product/213/2178).
 - If the process that consumes a lot of bandwidth is an exceptional process, there may be a virus or a Trojan. You can terminate the process yourself or use security software. You can also back up the data and reinstall the system.
 - If the process that consumes a lot of bandwidth is a Tencent Cloud component process, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category), and we will help you locate and troubleshoot the problem.


It is recommended to check the location of the destination IP on [What Is My IP Address](https://whatismyipaddress.com/). If the IP location is in other countries/regions, the security risk is larger. 


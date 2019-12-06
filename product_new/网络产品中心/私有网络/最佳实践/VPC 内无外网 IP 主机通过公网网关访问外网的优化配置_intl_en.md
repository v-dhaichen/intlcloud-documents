## Environment Description
If you need to access public networks, but some CVMs in your Tencent Cloud VPC do not have public IP addresses, then you can purchase public gateway CVMs and use them as the public network egress so that other CVMs without public IP addresses can access the Internet. These public gateway CVMs perform source address translation for outbound traffic. The source IP addresses of traffic by all other CVMs that access the public network are translated into the IP address of the public gateway after the traffic passes through the public gateway, as shown in the following figure.
![](https://main.qcloudimg.com/raw/b2fb63bfa8fc03cde6cedcde845a9b65.png)

To build the preceding architecture, you must complete the procedure shown in the following figure.
![](https://main.qcloudimg.com/raw/8fc0ad20600a2831b5a1b32ce1b66e0b.png)
## Architecture Building
### Creating a Gateway Subnet
A public gateway can only forward the route forwarding request of the subnet to which it does not belong. For this reason, a public gateway CVM cannot be in the same subnet as the CVM that needs to access the public network through the public gateway. To address this issue, you need to first set up a separate gateway subnet. <!--For the step-by-step procedure, see [Creating a Gateway Subnet]()-->
![](https://main.qcloudimg.com/raw/83b6487f44f451a40237e785e6d262c6.png)

### Purchasing a Public Gateway
For the step-by-step procedure for purchasing a public gateway in the gateway subnet that was just created.<!--see [Purchasing a Public Gateway]()-->

### Creating a Gateway Subnet Route Table
A gateway subnet and a common subnet cannot be associated with the same route table. A separate gateway route table needs to be created and associated with the gateway subnet. <!--For the step-by-step procedure, see [Creating a Gateway Subnet Route Table]()-->
![](https://main.qcloudimg.com/raw/af6228ca3acee55744453e1d3f9b962e.png)
![](https://main.qcloudimg.com/raw/3d4ef8d4404a3d70ca24a7cb8c793bf0.png)

### Configuring the Route Table of a Common Subnet
In the configuration of the route table of a common subnet, the default route is configured to go through the public gateway CVM so that the CVMs in the common subnet can access the public network with the route forwarding capability of the public gateway. <!--For the step-by-step procedure, see [Configuring a Common Subnet Route Table]()-->
![](https://main.qcloudimg.com/raw/6e9e84fcc6cd439137eda3476375fa1f.png)

## Configuration Optimization
A public gateway CVM sets the NAT rules of iptables by default and enables ip_forward of the kernel, with all the basic public gateway features enabled. We recommend that you use the following configuration method for achieving better performance.
1. Write the net.ipv4.ip_forward configuration to the **/etc/sysctl.conf** file by running the following command:
```
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
```
2. Increase the value of the `nf_conntrack` configuration parameter by running the following commands:
```
echo "echo 1048576 > /proc/sys/net/netfilter/nf_conntrack_max" >> /etc/rc.local
echo "echo 262144 > /sys/module/nf_conntrack/parameters/hashsize" >> /etc/rc.local
```
3. Set NAT rules for forwarding.
```
echo "iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE" >> /etc/rc.local
```
4. Disable the timestamp option.
```
echo "iptables -t mangle -A POSTROUTING -p tcp -j TCPOPTSTRIP --strip-options timestamp" >> /etc/rc.local
```
5. Set the RPS of the public gateway.
 Create a script named **set_rps.sh** in the **/usr/local/sbin/** directory, and add the following code into the script:
```
#!/bin/bash
mask=0
i=0
cpu_nums=`cat /proc/cpuinfo |grep processor |wc -l`
if(($cpu_nums==0));then
	exit 0
fi
nic_queues=`cat /proc/interrupts |grep -i virtio0-input |wc -l`
if(($nic_queues==0));then
    exit 0
fi
echo "cpu number" $cpu_nums "nic queues" $nic_queues
mask=$(echo "obase=16;2^$cpu_nums - 1" |bc)
flow_entries=$(echo "$nic_queues * 4096" |bc)
echo "mask = "$mask
echo "flow_entries = "$flow_entries
#for i in {0..$nic_queues}
while (($i < $nic_queues))  
do
	echo $mask > /sys/class/net/eth0/queues/rx-$i/rps_cpus
	echo 4096 > /sys/class/net/eth0/queues/rx-$i/rps_flow_cnt
	i=$(($i+1)) 
done
echo $flow_entries > /proc/sys/net/core/rps_sock_flow_entries 
```
Run the following command after the script is created:
```
chmod +x /usr/local/sbin/set_rps.sh
echo "/usr/local/sbin/set_rps.sh" >> /etc/rc.local
```

After the preceding configuration, restart the public gateway CVM to make the configuration effective, and test whether the server with no public IP address can access the public network.

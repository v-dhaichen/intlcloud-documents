In this section, we will introduce to you about how to set up a fixed IP address for external access if the cluster requires to actively make external access.

## Required Conditions

If three conditions are satisfied in the cluster of your scaling group at the same time as follows:
- Requests are received from CLB;
- Cluster machines need to actively make external access;
- When making external access, it is desired to use a **fixed** public IP.

the IP address can be set up according to the following solution.

## Solution Overview
1. Receive and respond to external requests via CLB.
2. Place the machine in the subnet of VPC, direct the routing table to the NAT gateway and all active external request are delivered via the public IP of the NAT gateway.
3. The network attribute of the scaling group is set as this subnet, so that all the expanded machines will actively make external access via the NAT gateway.

The setting procedure is shown as follows:

![1](https://main.qcloudimg.com/raw/645411d191ecdf976ed11d5a11cd69aa.png)



## Setting Method

### Step One: Create a VPN and a Subnet

#### **1. Create a VPC**

1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), click "Virtual Private Cloud" in the navigation bar, or click "Experience" in Tencent Cloud's [VPC Overview Page](https://intl.cloud.tencent.com/product/vpc.html) to enter the [VPC Console](https://console.cloud.tencent.com/vpc/).

2. Select a region in the drop-down box above the list and click "New" to create a VPC. For example, select the region of "North China (Beijing)".

3. Enter names of the VPC and subnet as well as CIDR, and select the availability zone for the subnet.

4. Click "Create".


#### **2. Create a subnet**

1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), click "Virtual Private Cloud" in the navigation bar, and then click "Subnet" in the left navigation bar. Choose a region and VPC in the drop-down box.
![2](https://main.qcloudimg.com/raw/8c04a129eabe941ad8ef9758347e028f.png)

2. Click "New", and then enter the subnet name, CIDR, availability zone and associated routing table. After that, click "Create" to confirm.

3. After the creation is completed, you can purchase machines for this subnet.


### Step 2: Create a NAT gateway
#### **1. Purchase desired products**
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), select "Virtual Private Cloud" tab, and then select "NAT Gateway".

2. Click the "New" button at the upper left corner, and enter or specify the following parameters in the pop-up box:
  - Gateway name
	- Gateway type (which can be changed after creation)
	- VPC of the NAT Gateway service (which was just created by you)
	- Assign the elastic IP for the NAT gateway. This IP is the fixed IP via which your machine makes external access.

3. After selection, click "OK" to complete the creation of NAT gateway.

4. After the creation of the NAT gateway, you need to configure the routing rules on the Routing Table page of the VPC Console to direct the subnet traffic to the NAT gateway.

#### **2. Set the routing table (highlights)**
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), click "Virtual Private Cloud" in the navigation bar to enter the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=8), and then select "Routing Table".

2. In the routing table list, click the ID of the routing table associated to the subnet that needs to access the Internet to go to the details page of the routing table, and then click "Edit" button in the "Routing Policies".

3. Click "New Line" to fill in the destination (for example, "0.0.0.0/0" can be entered in this scenario), select "NAT Gateway" as the next hop type, select the created NAT gateway ID, and then click "OK".
![3](https://main.qcloudimg.com/raw/e5029e42a6570c26814375f2264a7f4b.png)

Now, even without public IP, your machine in this subnet can actively get external access via the fixed IP of the NAT gateway, during which this IP is shown to be fixed externally.

Even if I purchase a CVM without any public IP and with the bandwidth of zero, I still can actively make external access, which is shown as follows:

![4](https://mc.qcloudimg.com/static/img/17ed153e06272885b56764781d9ab581/49.jpg)

However, the scaling group needs to identify this subnet and ensure that all the machines are created on this subnet.

### Step 3: Set up the scaling group
It is used to direct the subnet information to the scaling group so that the newly expanded machine can be installed in this subnet by the scaling group.
**In this way, the expanded machine will use the fixed exit IP address of the NAT gateway to access external websites.**

In the [Auto Scaling Console](https://console.cloud.tencent.com/autoscaling/config), click "New":

- Fill in the name of the scaling group, launch configuration (to be set up well in advance), maximum group size, minimum group size, initial number of instances, and other information.
- Select "Network" and "Subnet", and then direct them to the selected VPC and subnet **(important)**.

The setting procedure is shown as follows:

![5](https://main.qcloudimg.com/raw/f752a1ae61b9a49c97d50626f33f76da.png)

The setting has been completed.


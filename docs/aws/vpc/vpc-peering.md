# VPC Peering

Let us assume that there are two VPCs created in two different regions (One in N.Virginia and one in Mumbai).
There are few EC2 instances running in both VPCs.
If EC2 instances running in one VPC need to talk communicate to other EC2 instances running in another VPC,
then we need VPC peering.

![aws_112.png](../../assets/aws_112.png)

**Rules**

1. If one VPC from one region needs to talk to another VPC, VPC peering is needed.
2. Assume there are three VPCs (A, B, C). A is peering with B, B is peering with C. 
So, A cannot talk to C unless there is peering configured between A and C 
3. We can do VPC peering from VPC in one account to VPC in another account as well.

## Steps for VPC Peering

1. Create two VPCs in two different regions
2. Create subnets for each VPC
3. Create internet gateway for each VPC
4. Create route tables for each VPC
5. Create a security group for each VPC
6. Create EC2 instances for each VPC
7. Create VPC peering connection and associate them with VPC
8. Login and check connectivity


### Create two VPCs in two different regions

**For N.Virginia Region**

To do so, open the VPC services and click on the "Create VPC" button

![aws_113.png](../../assets/aws_113.png)

Update the fields as per snapshot. Then click on the "Create VPC" button.

![aws_114.png](../../assets/aws_114.png)

![aws_115.png](../../assets/aws_115.png)

**For Mumbai Region**

To do so, open the VPC services and click on the "Create VPC" button

![aws_113.png](../../assets/aws_113.png)

Update the fields as per snapshot. Then click on the "Create VPC" button.

![aws_116.png](../../assets/aws_116.png)

![aws_117.png](../../assets/aws_117.png)

### 2. Create subnets for each VPC

**For N.Virginia Region**

To do so, click on the "Subnets" menu and click on the "Create Subnet" button.

![aws_52.png](../../assets/aws_52.png)

Update the fields as per snapshot. 

![aws_118.png](../../assets/aws_118.png)

![aws_119.png](../../assets/aws_119.png)

**For Mumbai Region**

To do so, click on the "Subnets" menu and click on the "Create Subnet" button.

![aws_52.png](../../assets/aws_52.png)

Update the fields as per snapshot. 

![aws_120.png](../../assets/aws_120.png)

![aws_121.png](../../assets/aws_121.png)

## 3. Create internet gateway for each VPC and attach it with VPC

**For N.Virginia Region**

To do so, click on the "Internet gateways" menu and click on the "Create internet gateway" button.

![aws_59.png](../../assets/aws_59.png)

Update the fields as per snapshot. 

![aws_122.png](../../assets/aws_122.png)

Click on the "Create internet gateway" button

![aws_123.png](../../assets/aws_123.png)

Select the internet gateway created and click on the "Action" dropdown menu

![aws_124.png](../../assets/aws_124.png)

Update the fields as per snapshot. 

![aws_125.png](../../assets/aws_125.png)

Click on the "Attach internet gateway" button

![aws_131.png](../../assets/aws_131.png)

**For Mumbai Region**

To do so, click on the "Internet gateways" menu and click on the "Create internet gateway" button.

![aws_59.png](../../assets/aws_59.png)

Update the fields as per snapshot. 

![aws_126.png](../../assets/aws_126.png)

Click on the "Create internet gateway" button

![aws_127.png](../../assets/aws_127.png)

Select the internet gateway created and click on the "Action" dropdown menu

![aws_128.png](../../assets/aws_128.png)

Update the fields as per snapshot. 

![aws_129.png](../../assets/aws_129.png)

Click on the "Attach internet gateway" button

![aws_130.png](../../assets/aws_130.png)


### 4. Create route tables for each VPC

**For N.Virginia Region**

To do so, click on the "Route tables" menu and click on the "Create route table" button.

![aws_65.png](../../assets/aws_65.png)

Update the fields as per snapshot

![aws_132.png](../../assets/aws_132.png)

Click on the "Create route table" button

![aws_133.png](../../assets/aws_133.png)

Click on the "Subnet association" tab. Click on the "Edit subnet association" button

![aws_134.png](../../assets/aws_134.png)

Select subnet and click on the "Save association" button

![aws_133.png](../../assets/aws_133.png)

Click on the "Routes" tab and click on the "Edit routes" button

![aws_150.png](../../assets/aws_150.png)

Click on the "Add route" button and update the fields like below

![aws_151.png](../../assets/aws_151.png)

Click on the "Save changes" button

**For Mumbai Region**

To do so, click on the "Route tables" menu and click on the "Create route table" button.

![aws_65.png](../../assets/aws_65.png)

Update the fields as per snapshot

![aws_135.png](../../assets/aws_135.png)

Click on the "Subnet association" tab. Click on the "Edit subnet association" button

![aws_136.png](../../assets/aws_136.png)

Select subnet and click on the "Save association" button

![aws_137.png](../../assets/aws_137.png)

Click on the "Routes" tab and click on the "Edit routes" button

![aws_152.png](../../assets/aws_152.png)

Click on the "Add route" button and update the fields like below

![aws_153.png](../../assets/aws_153.png)

Click on the "Save changes" button

### 5. Create a security group for each VPC

**For N.Virginia Region**

To do so, click on the "Security group" menu and click on the "Create security group" button

![aws_79.png](../../assets/aws_79.png)

Update the fields as per snapshot

![aws_138.png](../../assets/aws_138.png)

Click on the "Create security group" button

![aws_139.png](../../assets/aws_139.png)

**For Mumbai Region**

To do so, click on the "Security group" menu and click on the "Create security group" button

![aws_79.png](../../assets/aws_79.png)

Update the fields as per snapshot

![aws_140.png](../../assets/aws_140.png)

Click on the "Create security group" button

![aws_141.png](../../assets/aws_141.png)


### 6. Create EC2 instances for each VPC

**For N.Virginia Region**

To do so, open the "EC2" service. Click on the "Launch instance" button. 

![aws_86.png](../../assets/aws_86.png)

Update the fields as per snapshot. 

![aws_142.png](../../assets/aws_142.png)

Create a key pair

![aws_143.png](../../assets/aws_143.png)

Update the fields as per snapshot. 

![aws_144.png](../../assets/aws_144.png)

Click on the "Launch instance" button

![aws_145.png](../../assets/aws_145.png)


**For Mumbai Region**

To do so, open the "EC2" service. Click on the "Launch instance" button. 

![aws_86.png](../../assets/aws_86.png)

Follow the similar steps to launch EC2 instance like the Virginia region.

Create a key pair

![aws_147.png](../../assets/aws_147.png)

Update the fields as per snapshot. 

![aws_148.png](../../assets/aws_148.png)

Click on the "Launch instance" button

![aws-149.png](../../assets/aws-149.png)


### 7. Create VPC peering connection (in only one region) and associate them with VPC (in another region)

To do so, click on the "Peering connection" menu and click on the "Create peering connection" button

![aws_154.png](../../assets/aws_154.png)

Update the fields as per snapshot.

![aws_146.png](../../assets/aws_146.png)

Now VPC peering connection is created in the N.Virginia region.

![aws_155.png](../../assets/aws_155.png)

It needs to be accepted in the Mumbai region now.

![aws_156.png](../../assets/aws_156.png)

![aws_157.png](../../assets/aws_157.png)


### 8. Login and check connectivity

Connect the EC2 instance in the N.Virginia region

![aws_158.png](../../assets/aws_158.png)

![aws_159.png](../../assets/aws_159.png)

Pinging google.com works fine.

![aws_160.png](../../assets/aws_160.png)

We will try to connect the EC2 instance created in the Mumbai region from here.

![aws_161.png](../../assets/aws_161.png)

It is not able to connect.
So, VPC peering from N.Virginia region to the Mumbai region is not working.
The reason is that routing tables need to be modified to accept the subnet from both VPCs.

Update the routing table in the N.Virginia region. Add the subnet range of Mumbai region VPC.

![aws_162.png](../../assets/aws_162.png)

Update the routing table in the Mumbai region. Add the subnet range of N.Virginia region VPC.

![aws_163.png](../../assets/aws_163.png)

Now try to ping the EC2 instance from Virginia to Mumbai EC2 instance.
It works fine.

![aws_164.png](../../assets/aws_164.png)










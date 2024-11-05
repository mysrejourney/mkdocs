# Creating Virtual Private Cloud (VPC)

To create VPC in AWS, there are steps to follow.

1. Create VPC and assign the CIDR block 
2. Create two subnets (one for public and one for private) in two different availability zones and assign the CIDR block for both subnets
3. Create Internet Gateway and attach it to VPC
4. Create two routing tables (one for public and one for private) and attach them with respective subnets
5. Map routing table created for public subnet with Internet Gateway
6. Create two security groups (one for public and one for private).
7. Update the inbound rules for a public security group and allow access to `0.0.0.0/0` for SSH, HTTP, HTTPS, RDP. 
8. Update the inbound rules for a private security group and allow access to a public security group created at step # 4
9. Create two EC2 instances (one for public and one for private) and map the respective security group
10. Login into EC2 instance created in public subnet and check the internet connectivity. This should connect the internet
11. Login into EC2 instance created in private subnet
    (You cannot log in directly as it is private. You have to connect public EC2 instance and from there,
    you can connect private EC2 instance) and check the internet connectivity. This should not connect the internet
12. Create NAT Gateway and attach it private routing table
13. Check if Elastic IP created
14. Login into EC2 instance created in private subnet and check the internet connectivity. This should connect the internet


Let us explore the steps now.

## 1. Create VPC and assign the CIDR block 

To do so, open the VPC services and click on the "Create VPC" button

![aws_49.png](../../assets/aws_49.png)

Update the fields as per snapshot. Then click on the "Create VPC" button.

![aws_50.png](../../assets/aws_50.png)

![aws_51.png](../../assets/aws_51.png)


 ## 2. Create two subnets (one for public and one for private) in two different availability zones and assign the CIDR block for both subnets

To do so, click on the "Subnets" menu and click on the "Create Subnet" button.

![aws_52.png](../../assets/aws_52.png)

Update the fields as per snapshot. This is for public subnet

![aws_53.png](../../assets/aws_53.png)

Click on the "Create Subnet" button

![aws_54.png](../../assets/aws_54.png)

![aws_55.png](../../assets/aws_55.png)

Update the fields as per snapshot. This is for private subnet

![aws_56.png](../../assets/aws_56.png)

Click on the "Create Subnet" button

![aws_57.png](../../assets/aws_57.png)

![aws_58.png](../../assets/aws_58.png)

## 3. Create Internet Gateway and attach it to VPC

To do so, click on the "Internet gateways" menu and click on the "Create internet gateway" button.

![aws_59.png](../../assets/aws_59.png)

Update the fields as per snapshot.

![aws_60.png](../../assets/aws_60.png)

Click on the "Create internet gateway" button

![aws_61.png](../../assets/aws_61.png)

Select the internet gateway created and click on the "Action" dropdown menu

![aws_62.png](../../assets/aws_62.png)

Click on the "Attach to VPC" option

![aws_63.png](../../assets/aws_63.png)

Select the VPC (we created in the step # 1) and click on the "Attach internet gateway" button

![aws_64.png](../../assets/aws_64.png)

## 4. Create two routing tables (one for public and one for private) and attach them with respective subnets

To do so, click on the "Route tables" menu and click on the "Create route table" button.

![aws_65.png](../../assets/aws_65.png)

Update the fields as per snapshot. This is for public subnet.

![aws_66.png](../../assets/aws_66.png)

Click on the "Create route table" button

![aws_67.png](../../assets/aws_67.png)

To do so, click on the "Route tables" menu and click on the "Create route table" button.

![aws_65.png](../../assets/aws_65.png)

Update the fields as per snapshot. This is for private subnet.

![aws_68.png](../../assets/aws_68.png)

Click on the "Create route table" button

![aws_69.png](../../assets/aws_69.png)

#### Attach routing table with respective subnets

To do so, select the public routing table and click on the "Subnet Association" tab

![aws_70.png](../../assets/aws_70.png)

Click on the "Edit subnet association" button

![aws_71.png](../../assets/aws_71.png)

Select the public subnet created and click on the "Save association" button

![aws_72.png](../../assets/aws_72.png)

Repeat the same steps for private routing table.

![aws_73.png](../../assets/aws_73.png)

## 5. Map public routing table with Internet Gateway

To do so, click on the "Route tables" menu and select the public routing table

![aws_74.png](../../assets/aws_74.png)

Click on the "Routes" tab

![aws_75.png](../../assets/aws_75.png)

Click on the "Edit routes" button

![aws_76.png](../../assets/aws_76.png)

Click on the "Add route" button, and the destination value is "0.0.0.0/0," select the "internet gateway"
and then select the internet gateway we created from the option.

![aws_77.png](../../assets/aws_77.png)

Click on the "Save changes" button.

![aws_78.png](../../assets/aws_78.png)

## 6. Create two security groups (one for public and one for private).

To do so, click on the "Security group" menu and click on the "Create security group" button

![aws_79.png](../../assets/aws_79.png)

## 7. Update the inbound rules for a public security group and allow access to `0.0.0.0/0` for SSH, HTTP, HTTPS, RDP. 

Update the fields as per snapshot and click on the "Add rule" button for inbound rules.
This is for public security group.

![aws_80.png](../../assets/aws_80.png)

Add the rules as per screenshot.

![aws_81.png](../../assets/aws_81.png)

Click on the "Create security group" button

![aws_82.png](../../assets/aws_82.png)

Click on the "Security group" menu and click on the "Create security group" button

![aws_79.png](../../assets/aws_79.png)

## 8. Update the inbound rules for a private security group and allow access to a public security group created at step # 4

Update the fields as per snapshot and click on the "Add rule" button for inbound rules.
This is for private security group.

![aws_83.png](../../assets/aws_83.png)

Add the rules as per snapshot.

![aws_84.png](../../assets/aws_84.png)

Click on the "Create security group" button

![aws_85.png](../../assets/aws_85.png)

## 9. Create two EC2 instances (one for public and one for private) and map the respective security group

To do so, open the "EC2" service. Click on the "Launch instance" button. This is for public instance

![aws_86.png](../../assets/aws_86.png)

Update the fields as per snapshot. 

![aws_87.png](../../assets/aws_87.png)

Create a new key pair for secured login.

![aws_88.png](../../assets/aws_88.png)

Under network settings, click on the "Edit" button and update the details as per snapshot.

![aws_89.png](../../assets/aws_89.png)

Click on the "Launch instance" button

![aws_90.png](../../assets/aws_90.png)

Open the "EC2" service. Click on the "Launch instance" button. This is for private instance

![aws_86.png](../../assets/aws_86.png)

Update the fields as per snapshot

![aws_91.png](../../assets/aws_91.png)

Create a new key pair for secured login.

![aws_92.png](../../assets/aws_92.png)

Under network settings, click on the "Edit" button and update the details as per snapshot.

![aws_93.png](../../assets/aws_93.png)

Click on the "Launch instance" button

![aws_94.png](../../assets/aws_94.png)


## 10. Login into EC2 instance created in public subnet and check the internet connectivity.

Connect the public EC2 instance via terminal.

![aws_95.png](../../assets/aws_95.png)

![aws_96.png](../../assets/aws_96.png)

Now, check if you are able to connect `google.com`. You are able to connect the `google.com` website.

![aws_97.png](../../assets/aws_97.png)

## 11. Login into EC2 instance created in private subnet

You cannot log in directly as it is private. You have to connect public EC2 instance and from there, 
you can connect private EC2 instance

To do so, create the filename "my-private-ec2-instance-key.pem" in public EC2 instance.
Copy the content from key created for private EC2 instance to this above file.
Update the file permission.

![aws_98.png](../../assets/aws_98.png)

![aws_99.png](../../assets/aws_99.png)

Now, check if you are able to connect `google.com`. You are unable to connect the `google.com` website.

![aws_100.png](../../assets/aws_100.png)

## 12. Create NAT Gateway and attach it private routing table

To do so, open "VPC" services, click on the "NAT gateway" menu. Click on the "Create NAT gateway" button

![aws_101.png](../../assets/aws_101.png)

Update the fields as per snapshot.
Remember to choose public subnet because the internet will be provided from public to nat gateway.
Then click on "Allocate Elastic IP" button.

![aws_102.png](../../assets/aws_102.png)

Click on the "Create NAT gateway" button.

![aws_103.png](../../assets/aws_103.png)

![aws_104.png](../../assets/aws_104.png)

## 13. Check if Elastic IP created

Elastic IP will be automatically created now. This IP address will act as frontend for private subnets.

![aws_105.png](../../assets/aws_105.png)

### Attach NAT gateway with private routing table

Open the private routing table and click on "Route" tab. Then click on the "Edit routes" button.

![aws_106.png](../../assets/aws-106.png)

Update the fields as per snapshot.

![aws_107.png](../../assets/aws_107.png)

Click on the "Save changes" button

![aws_108.png](../../assets/aws_108.png)

## 14. Login into EC2 instance created in private subnet and check the internet connectivity.

Connect public EC2 instance and check the internet connection

![aws_109.png](../../assets/aws_109.png)

Connect private EC2 instance from public EC2 instance and check the internet connection

![aws_110.png](../../assets/aws_110.png)

Now the internet is flowing from end use to public EC2 and from public EC2 to private EC2 instance.




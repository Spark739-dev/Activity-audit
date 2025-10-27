# VPC CREATION IN AWS CLOUD ENVIRONMENT
## NAME:VESHWANTH.
## REG NO:212224230300
## Task 1: Create Your VPC
In this task, you will use the VPC and more option in the VPC console to create multiple resources, including a VPC, an Internet
Gateway, a public subnet and a private subnet in a single Availability Zone, two route tables, and a NAT Gateway.
4. In the search box to the right of Services, search for and choose VPC to open the VPC console.

5. Begin creating a VPC.
In the top right of the screen, verify that N. Virginia (us-east-1) is the region.
Choose the VPC dashboard link which is towards the top left of the console.
Next, choose Create VPC .
Note: If you do not see a button with that name, choose the Launch VPC Wizard button instead.

6. Configure the VPC details in the VPC settings panel on the left:
Choose VPC and more.
Under Name tag auto-generation, keep Auto-generate selected, however change the value from project to lab .
Keep the IPv4 CIDR block set to 10.0.0.0/16
For Number of Availability Zones, choose 1.
For Number of public subnets, keep the 1 setting.
For Number of private subnets, keep the 1 setting.
Expand the Customize subnets CIDR blocks section
Change Public subnet CIDR block in us-east-1a to 10.0.0.0/24
Change Private subnet CIDR block in us-east-1a to 10.0.1.0/24
Set NAT gateways to In 1 AZ.
Set VPC endpoints to None.
Keep both DNS hostnames and DNS resolution enabled.

7. In the Preview panel on the right, confirm the settings you have configured.
VPC: lab-vpc
**Subnets:**

us-east-1a
Public subnet name: lab-subnet-public1-us-east-1a
Private subnet name: lab-subnet-private1-us-east-1a
**Route tables**

lab-rtb-public
lab-rtb-private1-us-east-1a

**Network connections** 

lab-igw
lab-nat-public1-us-east-1a

8. At the bottom of the screen, choose Create VPC
The VPC resources are created. The NAT Gateway will take a few minutes to activate.
Please wait until all the resources are created before proceding to the next step.

9. Once it is complete, choose View VPC
The wizard has provisioned a VPC with a public subnet and a private subnet in one Availability Zone with route tables for each
subnet. It also created an Internet Gateway and a NAT Gateway.

To view the settings of these resources, browse through the VPC console links that display the resource details. For example,
choose Subnets to view the subnet details and choose Route tables to view the route table details. The diagram below
summarizes the VPC resources you have just created and how they are configured.
An Internet gateway is a VPC resource that allows communication between EC2 instances in your VPC and the Internet.
The lab-subnet-public1-us-east-1a public subnet has a CIDR of 10.0.0.0/24, which means that it contains all IP addresses
starting with 10.0.0.x. The fact the route table associated with this public subnet routes 0.0.0.0/0 network traffic to the internet
gateway is what makes it a public subnet.
<img width="753" height="351" alt="image" src="https://github.com/user-attachments/assets/986e3b8b-d0c5-4120-a904-a048e6411ef5" />

A NAT Gateway, is a VPC resource used to provide internet connectivity to any EC2 instances running in private subnets in the
VPC without those EC2 instances needing to have a direct connection to the internet gateway.
The lab-subnet-private1-us-east-1a private subnet has a CIDR of 10.0.1.0/24, which means that it contains all IP
addresses starting with 10.0.1.x.

## Task 2: Create Additional Subnets
In this task, you will create two additional subnets for the VPC in a second Availability Zone. Having subnets in multiple Availability
Zones within a VPC is useful for deploying solutions that provide High Availability.
After creating a VPC as you have already done, you can still configure it further, for example, by adding more subnets. Each subnet
you create resides entirely within one Availability Zone.

10. In the left navigation pane, choose Subnets.
First, you will create a second public subnet.

12. Choose Create subnet then configure:
VPC ID: lab-vpc (select from the menu).
Subnet name: lab-subnet-public2
Availability Zone: Select the second Availability Zone (for example, us-east-1b)
IPv4 CIDR block: 10.0.2.0/24
The subnet will have all IP addresses starting with 10.0.2.x.

13. Choose Create subnet
The second public subnet was created. You will now create a second private subnet.

14. Choose Create subnet then configure:
VPC ID: lab-vpc
Subnet name: lab-subnet-private2
Availability Zone: Select the second Availability Zone (for example, us-east-1b)
IPv4 CIDR block: 10.0.3.0/24
The subnet will have all IP addresses starting with 10.0.3.x.
15. Choose Create subnet
The second private subnet was created.
You will now configure this new private subnet to route internet-bound traffic to the NAT Gateway so that resources in the second
private subnet are able to connect to the Internet, while still keeping the resources private. This is done by configuring a Route
Table.
A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. Each subnet in a
VPC must be associated with a route table; the route table controls routing for the subnet.

16. In the left navigation pane, choose Route tables.
17. Select the lab-rtb-private1-us-east-1a route table.
Note: If the newly created routes are not visible, choose refresh button at the top to update the list of routes.
18. In the lower pane, choose the Routes tab.
Note that Destination 0.0.0.0/0 is set to Target nat-xxxxxxxx. This means that traffic destined for the internet (0.0.0.0/0) will be
sent to the NAT Gateway. The NAT Gateway will then forward the traffic to the internet.
This route table is therefore being used to route traffic from private subnets.
19. Choose the Subnet associations tab.
You created this route table in task 1 when you chose to create a VPC and multiple resources in the VPC. That action also
created lab-subnet-private-1 and associated that subnet with this route table.
Now that you have created another private subnet, lab-subnet-private-2, you will associate this route table with that subnet as
well.
20. In the Explicit subnet associations panel, choose Edit subnet associations
21. Leave lab-subnet-private1-us-east-1a selected, but also select lab-subnet-private2.
22. Choose Save associations
You will now configure the Route Table that is used by the Public Subnets.
23. Select the lab-rtb-public route table (and deselect any other subnets).
24. In the lower pane, choose the Routes tab.
Note that Destination 0.0.0.0/0 is set to Target igw-xxxxxxxx, which is an Internet Gateway. This means that internet-bound
traffic will be sent straight to the internet via this Internet Gateway.
You will now associate this route table to the second public subnet you created.
25. Choose the Subnet associations tab.
26. In the Explicit subnet associations area, choose Edit subnet associations
27. Leave lab-subnet-public1-us-east-1a selected, but also select lab-subnet-public2
28. Choose Save associations
Your VPC now has public and private subnets configured in two Availability Zones. The route tables you created in task 1 have
also been updated to route network traffic for the two new subnets.

<img width="739" height="361" alt="image" src="https://github.com/user-attachments/assets/6f29591b-5b17-4ade-b858-fddb094ed3fe" />

## Task 3: Create a VPC Security Group
In this task, you will create a VPC security group, which acts as a virtual firewall. When you launch an instance, you associate one or
more security groups with the instance. You can add rules to each security group that allow traffic to or from its associated instances.
29. In the left navigation pane, choose Security groups.

30. Choose Create security group and then configure:
Security group name: Web Security Group
Description: Enable HTTP access
VPC: choose the X to remove the currently selected VPC, then from the drop down list choose lab-vpc

32. In the Inbound rules pane, choose Add rule

34. Configure the following settings:
Type: HTTP
Source: Anywhere-IPv4
Description: Permit web requests

36. Scroll to the bottom of the page and choose Create security group
You will use this security group in the next task when launching an Amazon EC2 instance.

## Task 4: Launch a Web Server Instance
In this task, you will launch an Amazon EC2 instance into the new VPC. You will configure the instance to act as a web server.

34. In the search box to the right of Services, search for and choose EC2 to open the EC2 console.

35. From the Launch instance menu choose Launch instance.
  
36. Name the instance:
Give it the name Web Server 1
When you name your instance, AWS creates a tag and associates it with the instance. A tag is a key value pair. The key for
this pair is *Name*, and the value is the name you enter for your EC2 instance.
37. Choose an AMI from which to create the instance:
In the list of available Quick Start AMIs, keep the default Amazon Linux selected.
Also keep the default Amazon Linux 2023 AMI selected.
The type of Amazon Machine Image (AMI) you choose determines the Operating System that will run on the EC2 instance
that you launch.

38. Choose an Instance type:
In the Instance type panel, keep the default t2.micro selected.
The Instance Type defines the hardware resources assigned to the instance.
39. Select the key pair to associate with the instance:
    
From the Key pair name menu, select vockey.
The vockey key pair you selected will allow you to connect to this instance via SSH after it has launched. Although you will
not need to do that in this lab, it is still required to identify an existing key pair, or create a new one, or choose to proceed
without a key pair, when you launch an instance.

40. Configure the Network settings:
Next to Network settings, choose Edit, then configure:
Network: lab-vpc
Subnet: lab-subnet-public2 (not Private!)
Auto-assign public IP: Enable
Next, you will configure the instance to use the Web Security Group that you created earlier.
Under Firewall (security groups), choose Select existing security group.
For Common security groups, select Web Security Group.
This security group will permit HTTP access to the instance.
41. In the Configure storage section, keep the default settings.
    
Note: The default settings specify that the root volume of the instance, which will host the Amazon Linux guest operating system
that you specified earlier, will run on a general purpose SSD (gp3) hard drive that is 8 GiB in size. You could alternatively add
more storage volumes, however that is not needed in this lab.

42. Configure a script to run on the instance when it launches:
Expand the Advanced details panel.
Scroll to the bottom of the page and then copy and paste the code shown below into the User data box:

<img width="790" height="276" alt="image" src="https://github.com/user-attachments/assets/cf4a5ee9-772e-4636-9184-026281370db5" />

43. At the bottom of the Summary panel on the right side of the screen choose Launch instance
You will see a Success message.

45. Choose View all instances
46. Wait until Web Server 1 shows 2/2 checks passed in the Status check column.
This may take a few minutes. Choose the refresh icon at the top of the page every 30 seconds or so to more quickly become
aware of the latest status of the instance.
You will now connect to the web server running on the EC2 instance.
47. Select Web Server 1.
48. Copy the Public IPv4 DNS value shown in the Details tab at the bottom of the page.
49. Open a new web browser tab, paste the Public DNS value and press Enter.
You should see a web page displaying the AWS logo and instance meta-data values.
The complete architecture you deployed is:

<img width="764" height="407" alt="image" src="https://github.com/user-attachments/assets/8e020874-e780-43a7-8b8a-a0d2a9501fd7" />

## OUTPUT:
<img width="1155" height="622" alt="image" src="https://github.com/user-attachments/assets/7bee7920-0c8c-4a43-a3e8-30e373d0fb81" />
<img width="1157" height="621" alt="image" src="https://github.com/user-attachments/assets/2bb730b9-70a0-465f-ab74-382028804255" />
<img width="1154" height="619" alt="image" src="https://github.com/user-attachments/assets/763ecea8-4d3c-4260-b9bf-168126994639" />

## RESULT:

The Virtual Private Cloud is successfully implemented and created Successfully in the AWS cloud Environment.

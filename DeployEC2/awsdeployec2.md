 # Key Steps Are:

Setup Key Pair for EC2 and Download PEM file.
Create VPC:  cmpe281 (Using Wizard).
Launch EC2 Instance.
Connect to EC2 Instance.
PHP Setup on EC2 Linux AMI.
PHP Test.
Create PHP AMI Image.

# SETUP - CREATE EC2 KEY PAIR & ELASTIC IP

In the EC2 Dashboard for Region: US West (N. California), create an EC2 Key Pair named:  cmpe281-us-west-1
Download the Key Pair to your local machine and set it's permissions appropriately
In the EC2 Dashboard, Elastic IP section, allocate a new Elastic IP in VPC Scope.


# PART 1 - CREATE VPC

Go to the VPC Dashboard and Start the VPC Wizard in Region:  US West (N. California) -- i.e. Region: us-west-1.

VPC NAME:  CMPE281
WIZARD OPTION:  Public with Private Subnets
Elastic IP: The Elastic IP you created in SETUP Step.

After VPC is created, Set Up a Visual Ops account, Link your AWS Account to it, and then Import the CMPE281 VPC.
Select App Usage: Testing
Make sure to select "check-box" for:  Monitor and report external resource change of this app
    Creates:  A /16 network with two /24 subnets. 
    Public subnet instances use Elastic IPs to 
    access the Internet. 
    
    Do not select this option:
    Private subnet instances access the Internet 
    via Network Address Translation (NAT).  
    (Hourly charges for NAT devices apply.)
    Instead, select this option (to avoid charges to your account):
    In "Specify the details of your NAT gateway" Section,
    Select "Use NAT Instance Instead".  
    NAT Instance Type:          t2.micro
    NAT Instance Keypair:       cmpe281-us-west-1

    CIDR block                  10.0.0.0/16 
    IP range                    0.0.0.0 - 10.0.255.255   
    Subnet Mask                 255.255.0.0  
    IP Quantity                 65536   

    Public Subnet:              10.0.0.0/24
    Network =                   10.0.0.0
    Usable IPs =                10.0.0.1 to 10.0.0.254 for 254
    Broadcast =                 10.0.0.255
    Netmask =                   255.255.255.0
    Wildcard Mask =             0.0.0.255

    Private Subnet:             10.0.1.0/24
    Network =                   10.0.1.0
    Usable IPs =                10.0.1.1 to 10.0.1.254 for 254
    Broadcast =                 10.0.1.255
    Netmask =                   255.255.255.0
    Wildcard Mask =             0.0.0.255

# PART 2 - LAUNCH EC2 INSTANCE & CREATE AMI

Launch a new EC2 Instance into your CMPE281 VPC as follows:
Amazon Linux AMI 
T2 Micro Instance
VPC: cmpe281
Public Subnet
Auto Assign Public IP
Security Group: cmpe281-dmz (create new)
    Open Ports: 22, 80, 443
Select Key Pair: cmpe281-us-west-1
AWS Instance Name:  aws-php
Then, following instructions in the Lab Notes in GitHub (Links to an external site.)Links to an external site., Install PHP/LAMP Stack in your new EC2 Instance and Copy the Lab PHP Source Code into the Instance
Run the PHP Stress Test App and Observe the CPU Usage in AWS.
Shutdown your EC2 Instance and create a Linux AMI from the Setup.

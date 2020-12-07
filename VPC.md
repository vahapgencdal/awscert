# VPC Fundemantal
3 questions of exam will come from VPC
## VPC & Subnets Primer
VPC: private network to deploy your resources (regional resource)
* Subnets allow you to partition your network inside your VPC (Availability Zone resource)
* A public subnet is a subnet that is accessible from the internet
* A private subnet is a subnet that is not accessible from the internet
* To define access to the internet and between subnets, we use Route Tables.  
VPC Diagram  
![VPC](/images/VPC-DIAGRAM.PNG "VPC")


## Internet Gateway & NAT Gateways
Internet Gateways helps our VPC instances connect with the internet.  
**NAT Gateways** (AWS-managed) & **NAT Instances** (self-managed) allow your instances in your Private Subnets to access the internet while remaining private
![IG-NAT](/images/IG-NAT.PNG "IG-NAT")
### Network ACL & Security Groups
* #### NACL (Network ACL)
  * A firewall which controls traffic from and to subnet
  * Can have ALLOW and DENY rules
  * Are attached at the Subnet level
  * Rules only include IP addresses
* #### Security Groups
  * A firewall that controls traffic to and from an ENI / an EC2 Instance
  * Can have only ALLOW rules
  * Rules include IP addresses and other security groups
### VPC Flow Logs
Capture information about IP traffic going into your interfaces:
* VPC Flow Logs
* Subnet Flow Logs
* Elastic Network Interface Flow Logs
* VPC Flow logs data can go to S3 / CloudWatch Logs
## VPC Peering
* how we can establish connectivity between VPC and other structures. So, the first thing is called VPC peering. So say you have two virtual private clouds, they're either in two different accounts or in two different regions, and you wanna connect together as if they're part of the same network. So we want to connect to VPC, privately using V network from AWS.
* Must not have overlapping CIDR (IP address range)
* VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another)
* Transitive mean What I mean is that, if we connect VPC C, through a VPC peering connection between A and C, B and C cannot talk to each other, there is no transitivity in the VPC peering.
* Each VPC peering for between two VPC. if there is three VPC you need three Peering

![VPC-PEERING](/images/VPC-PEERING.PNG "VPC-PEERING")

## **VPC Endpoints**
So, Endpoints allow you to connect to AWS services, using a private network instead of using the public Internet network. So something you maybe didn't know is that all the AWS services are public.
* This gives you enhanced security and lower latency to access AWS services  
* We have a private subnet and an EC2 instance in it, and he wants to access Amazon S3 and DynamoDB, which are outside of the VPC into the public realm. Then we can create a VPC Endpoint gateway, and this is only for S3 and DynamoDB.
* a VPC Endpoint interface in your private subnet and through that invoice interface with an ENI we have private access to CloudWatch. So VPC Endpoints are really, really helpful anytime you need private access from within your VPC
![VPC-ENDPOINTS](/images/VPC-ENDPOINTS.PNG "VPC-ENDPOINTS")
## Site to Site VPN & Direct Connect
* Site to Site VPN
  * Connect an on-premises VPN to AWS
  * The connection is automatically encrypted
  * Goes over the public internet
* Direct Connect (DX)
  * Establish a physical connection between on- premises and AWS
  * The connection is private, secure and fast
  * Goes over a private network
  * Takes at least a month to establish
* Note: Site-to-site VPN and Direct Connect cannot access VPC endpoints 
## VPC Closing Comments
* VPC: Virtual Private Cloud
* Subnets:Tied to an AZ, network partition of the VPC
* Internet Gateway: at the VPC level, provide Internet Access
* NAT Gateway / Instances: give internet access to private subnets
* NACL: Stateless, subnet rules for inbound and outbound
* Security Groups: Stateful, operate at the EC2 instance level or ENI
* VPC Peering: Connect two VPC with non overlapping IP ranges, non transitive
* VPC Endpoints: Provide private access to AWS Services within VPC
* VPC Flow Logs: network traffic logs
* Site to Site VPN: VPN over public internet between on-premises DC and AWS
* Direct Connect: direct private connection to a AWS
## Typical 3 tier solution architecture
![THREE-TIER-ARCH](/images/THREE-TIER-ARCH.PNG "THREE-TIER-ARCH")
### LAMP Stack on EC2
* Linux: OS for EC2 instances
* Apache: Web Server that run on Linux (EC2)
* MySQL: database on RDS
* PHP: Application logic (running on EC2)
* Can add Redis / Memcached (ElastiCache) to include a caching tech
* To store local application data & software: EBS drive (root)
## Wordpress on AWS
![WORDPRESS-AWS](/images/WORDPRESS-AWS.PNG "WORDPRESS-AWS")
## Wordpress on AWS Full Image
![WORDPRESS-AWS-FULL](/images/WORDPRESS-AWS-FULL.PNG "WORDPRESS-AWS-FULL")

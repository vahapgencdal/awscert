# AWS Developer Certification

## 1.  The Budget Setup
This is to monitor if you go over the free tier and if that's the case, you will get an email alert and that will be great for you not to overspend some money.  
### [My Billing Dashboard -> Budgets](https://console.aws.amazon.com/billing/home)
* Cost Budget  
Here shortly defining your budget name and timeframe then Specify your monthly budget. if need add some additional parameters.  
Is using general purpose in all of your services budget monthly cost = some amount. please send some alerts.
* Usage budget  
difference between Cost budget here you are going to choose any usage type groups.  
for example : if you choose EC2:running hours; it will check just your EC2 cost and send mail.
* Reservation budget  
that is really using for reservation. you are going to reserv any service and in 72 hours you will get reserved alerts. here you are choosing if your reservation is completed or get some percent send some mails.
* Savings Plans budget
here you are going to track your services and look how much money you can cover or save. it is not available yet.
### [My Billing Dashboard -> Budget Reports](https://console.aws.amazon.com/billing/home)
here you are going to choose a budget with specified time; monthly, daily . then it will create report for you. with that you can see where did you spend your money with detail.

## 2.  The AWS Regions 
AWS is a global cloud provider, and therefore it has many data centers all around the world. And these are called Regions. a region is a cluster of data centers. 
*  most of the AWS services are region-scoped. 

### **The Availability Zones(AZ)**
Each region can have many availability zones. 

here's an example, for the region ap-southeast-2 which represents the Sydney region.

Then we're going to have three AZ,

* the first one is ap-southeast-2a
* the second one is ap-southeast-2b
* the third one is ap-southeast-2c.  

As you can see regions have numbers and AZ have letter after region.

Okay, so what is an AZ? 

![The Availibility Zones](/images/AZ.png "The Availibility Zones")

Each AZ is one or more discrete data centers,

And each data center will have redundant power,networking and connectivity. But all these AZ or availability zones are separate from each other, and that's why they're isolated from disasters.

So the AZ ap-southeast-2a is distinct and geographically isolated from 2b and 2c, okay. But even though they're geographically distant, and isolated from disasters, they're still connected with one another with high bandwidth ultra-low latency networking.

So we have a connectivity between all the availability zones.

## 3.  The Identity and Access Management (IAM) Service
As we can expect from the name that basically means users. So the whole of your AWS security is going to be in IAM. There's gonna be users, groups, roles and permissions. Here we are going to use root account is the main account. it is just one and then we will create user xxx by root user. then we will use the xxx account for training. 
* with IAM we are going to create policies and these policies will be written in JSON.

![The IAM](/images/IAM.png "The IAM")

 Now users can be grouped together  and group is whatever you want it to be but usually it's by functions, for example admin, devops or by teams, such as engineering, design or anything you want.
 you can apply permissions to groups and users will inherit these permissions.

Finally we have roles.
roles are only for internal usage within the AWS resources and services, okay. So roles is what we're going to give to machines.
Users is going to be for a physical person and roles is going to be for a machine. Iam is very handy if you want to manage your users. 

MFA is Multi-factor authentication. is using for extra security for example use google authenticator.

####The Steps
1. Create User 
2. Define User Details.
3. Select AWS access type. Programatic and Management Console
4. Set Console Password.
5. Set permissions.
    here you can create group or you can attach existing policies directly. when you create group the user you choosed will be defined under the group. and you are going to attach policies to the group. thus all the users will get the policies.
6. Then you are going to define tag.
    your account id is in your sign-in link :
    https://048XXXXXXXXX.signin.aws.amazon.com/console. here the number start with 048 is your account number.
7. you can change user password policies under Account Setting.

## 4. The EC2
 EC2 is basicly servers. when you try to lunch a EC2 basicly you are going to create a Virtual Server.
 it mainly sonsist : 
 * Renting Virtual Machines(EC2)
 * Storing data on virtual drives(EBS)
 * Distributes load accross machines(ELB)
 * Scaling the services using an auto-scaling group(ASG)

1. So we will go to services part and search EC2 after we found we need to choose basic AMI(Amazon Machine images).
so in this example we will choose Amazon Linux 2 AMI.  
2. Then we are going to choose instance type. thats mean we are going to choose how powerfull machine you want. 
3. after next here we are to configure Details
    * Number of instance 1 if you want more it will create more instances from same settings.
    * we havent Custom VPC(Vitual private server) so use default one
    * Subnet, if you want your instances work in specific availibility zone then you can choose one.
    * Auto-assign Public IP will define a public ip for you with that your instance will be open to internet.
    * and you can skip remains will be advanced.
4. then we are going to choose storage, we can leave all choices same and go next
5. the tags is using find your services easily in that case you can give specific label for example:training instance
6. Security Group is behave like a firewall before your instance for example : you dont want to open xxx port to outside. here you change name of group also
7. review part and click Lunch; here you are going to create key pair for access your machine from SSH. dont give your key anybody or deploy public place. download them and Click Launch Instances

### Connect EC2 Instance
#### **Mac OS/Linux**
  1. copy your public ip in instnace-detail you will find it. and check from security groups port 22 open.
  2. ssh ec2-user@x.xx.xxx.xx when you run that in the first i will want key from you.
  3. so goto under the folder which one has your key and try to run below command
  4. ssh -i training-instance.pem ec2-user@x.xx.xxx.xx 
  5. in the first time you will get UNPROTECTED PRIVATE KEY FILE error.
  6. for fixing chmod 0400 training-instance.pem
  7. ssh -i training-instance.pem ec2-user@x.xx.xxx.xx again 
  8. now you are in
#### **Windows**  
  1.  after you install putty you need to open puttygen for transform .pem file to .ppk
  2.  after you load just click **save private key** button
  3.  open your putty again
  4.  copy ec2-user@x.xx.xxx.xx to the host part
  5.  save it like :aws-training-instance
  6.  then for referance ppk file goto SSH from left menu then Auth
  7.  in the right side **private key file for authentication**  browse and load ppk
  8.  then click open you will connect successfully
#### **Browser**  
   1. instance->actions->connect
   2. 
## 5. The Security Group   
Security groups, they're fundamental of the network security in AWS. They control how traffic will be allowed into your EC2 Machines.
and as such they are super important and fundamental of Security. 

![The Security Group](/images/SC.png "The SC")

SC is using for control the inbound and the outbound traffic.
**for example** : lets go to our default security group and open inbound section and try to remove SSH rule.  
**what we are going to do?**  now we have no more inbound rules into our machine. Now what happens is that if we go ahead and try to SSH again, while the port 22 is not allowed and as you can see we'll just wait wait and time out.  
* Security groups are locked down to a region/VPC combination
* if you switch to another region, you have to create a new security group
* if you create another VPC, you have to recreate the Security Groups.
* The security groups live outside the EC2.
* it's really a firewall outside your EC2 instance
* if you try to connect to any port and your computer just hangs and waits that's probably a security group issue
* if you get a "connection refused" error, then its an application error or its not launched.
* All inbound traffic is blocked by default
* all outbound traffic is authorised by default
## 6. Private vs Public IP(IPv4)
Networking is to sort of have IP, there is IPv4 and IPv6. AWS has support for IPv6 as well.

for example, my company
it has a private network, the private network, basically has a private IP range, and private IPs have this very specific way of being defined but basically, that means that all the computers within that private network can talk to one another using the private IP.
Whereas, when you touch an internet gateway, which is a public gateway, well, these instances also will get access to other servers, and so on and so that's a common pattern in AWS.

![The AWS - Company Network](/images/IP-NET.png "The Net")

Now, basically, if you have another company it will also have a private network and within the private network, every computer can talk to one another and maybe also have an internet gateway with an IP and basically can connect all over the internet and talk to other servers, okay.
### Elastic IPs
when you start and you stop an EC2 instance, it will change its public IP
if you have a fixed public IP for whatever reason for your instance, what you are going to need is something called an Elastic IP.
So the Elastic IP is what, it's a public IPv4 and you own it, as long as you don't delete it.
*  it's quite an uncommon pattern, because you can only have five Elastic IP in your accounts
*  Overall, I would recommend to try avoiding using Elastic IP. they're often referred very poor architectural decisions
*  Instead of Elastic IP, you should use a random public IP and assign a DNS name to it.
*  we can also use a Load Balancer and not using public IP
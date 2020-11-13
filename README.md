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

#### The Steps
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
### Practice
* we cannot use that private IP to access my instances. when we try you will get timeout error. because it is private ip of AWS private network and you are trying to access from personal network
* in ec-2 instance type **ifconfig -a** you will get information of network.
* when you try stop and start instance you will see new public-ip
* for stable public-ip goto **Elastic-ip addresses** menu.
* Allocate elastic ip address from Amazon's pool. there you are a stable public-ip
* then goto **Actions->Associate Elastic ip address**
* and then choose your instance and Click **Associate**
* then when you restart instance you will see public-ip is not going to change
* then deassociate your elastic ip and release Elastic IP because AWS charging money for elastic-ip
## 6. Launc an Apache Server on EC2
 we are actually going to use our EC2 instance to launch an Apache Server on it.
So, we'll install an Apache Web Server, and we'll basically display a web page, and for this web page we'll just create
something called index.html, that will show the hostname of our machine.  
  1. First we are going to connect our instance with our public-ip 
  2. **sudo su** and this will basically elevate my rights on the machine.
  3. **yum update -y** This basically forces my machine to update itself.
  4. **yum install -y httpd.x86_64** this will install apache httpd for us
  5. **systemctl start httpd.service** will start httpd service
  6. **systemctl enable httpd.service** will enable httpd service
  7. **curl localhost:80** you will see the html result
  8. you can access from browser but you need to change security group. because it just allow SSH and port to
  9. goto to your training-security group which assigned your instance and then add new inbound rule select http and 80 port then save
  10. you can see which security-group assigned your instance from security part.
  11. lets change html
  12. echo "Hello World from $(hostname -f)" > /var/www/html/index.html
  13. and goto your browser and type public_ip:80. you should see 'hello world' html
   
## 7. EC2 User Data
it is possible to bootstrap our instances using an EC2 user data script. Well, bootstrapping means launching commands when the machine starts.
So, that script is only run once and when it first starts.
when you boot your instance? 
Well you want to install updates, install software, download common files from the internet, or anything you can think of, really.
* we regoing to terminate our instance create new instance and update instance and download apache http
* when you come **Configure instance detail** goto ** Advanced details ** and paste below scripts there  
    ```script
    #!/bin/bash

    ########################################################
    ##### USE THIS FILE IF YOU LAUNCHED AMAZON LINUX 2 #####
    ########################################################

    # get admin privileges
    sudo su

    # install httpd (Linux 2 version)
    yum update -y
    yum install -y httpd.x86_64
    systemctl start httpd.service
    systemctl enable httpd.service
    echo "Hello World from $(hostname -f)" > /var/www/html/index.html
    ``` 
* after your instance launched goto browser and you will see your 'Hello World' html.
## 8. EC2 instance Launch Types
they're very important for you to know going to the exam to understand which type of launch will allow you.
* **On Demand Instances** 
these are the type of instances we've been using from the beginning. So that when we create an instance,
and we have it right away, they're on demand. And it's great when you have a short workload, and want you to have predictable pricing, you get an hourly pricing ahead of time.
  1. Pay for what you use(billing persecond, after the first minute)
  2. has the highest cost but no upfront payment
  3. No long term commitment
* **Reseverved Instances**  
    Minimum 1 year instances; if you run some instances for a known amount of time, for example, you know that at least for one year, because maybe you run a database on it, then you should use a reserved instance type.  
     * Up to 75% discount compared to On-demand 
     * Pay upfront for what you use with long term commitment 
     * Reservation period can be 1 or 3 years 
     * Reserve a specific instance type 
     * Recommended for steady state usage applications (think database)
    1. **Convertible Reserved Instances**: 
     in which instead of saying you want a M four X large for one year, you're saying I want something for one year, and you can convert what that something is. So maybe it's an M four X large today, but maybe it's going to be a C five large tomorrow.
       * can change the EC2 instance type 
       * Up to 54% discount
    2. **Scheduled reserved instances**: 
    hey, I wanna have that instance every Thursday between three and 6:00 pm because I know I'm going to run some job between this time, but other than that, I don't need it. 
       * launch within time window you reserve 
       * When you require a fraction of day / week / month
* **Spot Instances**  
     it's going to be for short workloads, they're going to be very, very cheap, but the risk is that you can lose the instance, and that makes spot instances less reliable.
     * Can get a discount of up to 90% compared to On-demand
     * Instances that you can “lose” at any point of time if your max price is less than the
        current spot price
     * The MOST cost-efficient instances in AWS
     * Useful for workloads that are resilient to failure (Batch Jobs, Data Analyst ...)
     * Not great for critical jobs or databases
     * Great combo: Reserved Instances for baseline + On-Demand & Spot for peaks
* **Dedicated Instances**  
    we have dedicated instances where we know that no other customers will share the hardware, the underlying hardware on AWS.  
    * instances running on hardware that’s dedicated to you
    * May share hardware with other instances in same account
    * No control over instance placement (can move hardware after Stop / Start)
* **Dedicated Host**  
  where you actually book the entire physical server, and you control instance placements.
    * Physical dedicated EC2 server for your use
    * Full control of EC2 Instance placement
    * Visibility into the underlying sockets / physical cores of the hardware
    * Allocated for your account for a 3 year period reservation
    * More expensive
    * Useful for software that have complicated licensing model (BYOL – Bring Your Own License)
    * Or for companies that have strong regulatory or compliance needs
### **Which host is right for me?**
*  On demand: coming and staying in resort whenever we like, we pay the full price
* Reserved: like planning ahead and if we plan to stay for a long time, we may get a good discount.
* Spot instances: the hotel allows people to bid for the empty rooms and the highest bidder keeps the rooms. You can get kicked out at any time
* Dedicated Hosts: We book an entire building of the resort
### **EC2 Pricing**
* EC2 instances prices (per hour) varies based on these parameters 
    * Region you’re in
    * Instance Type you’re using
    * On-Demand vs Spot vs Reserved vs Dedicated Host
    * Linux vs Windows vs Private OS (RHEL, SLES, Windows SQL)
* You are billed by the second, with a minimum of 60 seconds. 
* You also pay for other factors such as storage, data transfer, fixed IP public addresses, load balancing
* You do not pay for the instance if the instance is stopped

if you goto Instances you will see all instance type on left menu
## 8. Elastic Network Interfaces (ENI)

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

[logo]: /images/AZ.png "Availability Zones" 


Each AZ is one or more discrete data centers,

And each data center will have redundant power,networking and connectivity. But all these AZ or availability zones are separate from each other, and that's why they're isolated from disasters.

So the AZ ap-southeast-2a is distinct and geographically isolated from 2b and 2c, okay. But even though they're geographically distant, and isolated from disasters, they're still connected with one another with high bandwidth ultra-low latency networking.

So we have a connectivity between all the availability zones.

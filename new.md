DOCUMENTATION FOR Autoscaling and Load Balancing :

<img src ="AScale.png">

Application Load Balancer 

1) Autoscaling automatically adjusts the amount of computational resources 
   based on the server load
2) Load Balancing distributes traffic between EC2 instances so that no one
   instance gets overwhhelmed.

First the planning is done -- then we will build it.
Autoscalling group helps us scale on demand and the load balancer -balances 
the instances actively available.



When we create an autoscaling group we need to pland and design in advance and we
need to decide :

1) the min  - 2- number of isntances which we would like to run.
2) max number -3-  : when the traffic increases how many more instances would you like to 
   spin up ; 
3) desired -2 - 


IMPORTANT : to resolve the problem of single point failure we need to run min 2;

So if there is a porblem the load balancer should stop sending traffic to the inactive 
instance and redirect all the traffic to the instance which is responding.
( STATUS CODE: 200 )

Autoscling group terminates that instance and replaces it with  the new instance.

As soon as the other instance becomes available, the Load Balancer redirects the traffic
to that instance.


So if there are 2 EC2 instances dealing with a lot of traffic, if one is not working anymore
Load Balancer is notified and redirect the traffic to the other EC2 instance.
Auto Scalling group is generating a instance and notifies the Load balancer to redirect
the traffic between the 2 instances.


When creating the group we need to decide the min and max number of instances running.
If the traffic increases : scale out.
When the traffic goes down : scale in.



When creating the instances we can create a template -- which can be used for all of them--


There are a few things which we need to consider in order to create :auto-scaling group and load balancer:

1) Launch template
2) Type of Load Balancer : we choose application load balancer ( for a web appp)
 with target group/listener group HTTP ( the load balancer si dealing with an external traffic which is form of HTTP-
 the load balancer needs to be able to listen to that -accept the request and foward it on ) 

3) create an application load balancer - attach the required dependecies;
4) auto-scaling group - attach this to LB;


So a lot of services are connected to each other ; 
<img src = "CWatch.png">



For all these services we need :

1) app running 
2) monitoring in place -- which triggers the notification so that we ;
3) attach the autoscaling gorup 
4) make it highliy available and scalable

The instances created are on differnt availability zones : if one zone is not working,
the traffic will be redirected


What the auto-scaling group will do ,it will do by following the given instruction in the
autoscaling availability policy and we create that in the beginning.


STEP1 : lunch the template

1) launch template name: eng114-bogdana
2) auto-scaling guidance -enable
3) ad tags
4) application and OS Images : Ubuntu 8.04
5) instance type : t2.micro ;
6) select the key : eng114 (this will be attached to all of these instances) 
7) in the security group select : the app security group ; 
8) in the Advance options  we include in the USER DATA the following script:
  
#!/bin/bash 

sudo apt-get update -y 
sudo apt-get update -y
sudo apt-get install nginx -y

sudo systemctl restart nginx
sudo systemctl enable nginx

=======
STEP2 : use this template to launch an autoscaling group together 
with the load balancer.

SELECT : autoscaling group :

1) Name the autoscaling group; 
2) Select the launch template which you have created
3) NetworK : default is Irland /other availability zones:
  eu-west -a1/eu-west-b1/eu-west-c1;
4) Attach a new load balancer > Application load balancer ;
5) Give it a name
6) Internet -facing
7) create a new target group with a  name for the Load Balancer
8) groups size : desired 2/min 2/max 3
9)scaling policy: metric type : average CPU utilization 
























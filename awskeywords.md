1.Lambda-severless 

2.Gartners magic quadrant -amazon is at at higher one 

3.Dedicated host -do not share with others 

4.Vendor lock in - use only one cloud and cannot shifted to other

5.private cloud -openstack,open nebula, eucalyptus-in 2011
 
6.AWS beanstalk -for deploying and scaling web application

7.Paas-aws beanstalk

8.Saas-zoho cloud

9.labs as a service -in AWS 

10.BMC-base board management controller 

11.RKT or rocket-containation use

12.Database -(oracle-biggest player) - solution of golden gates -use multimaster solution where in AWS we use ARORA

MASTER CLUSTER -

13.ECS-use dockerswarm in backend

EKS and ECS both cannot make server server less 

14.fargate over ECS/EKS-BACKND IS VANILLA or hardware.make the sever sever less.

15.S3(Amazon simple storage service)-

~Block storage-those can be formatted later time and attach with operating system.ex:elastic block store (EBS)-provide

volume to EC2

~Object storage -cannot be formatted.ex:S3- MAKE BUCKET -

16.RAID(redundancy array of independent disk)

~RAID 0 -MIRRORING(write on both disk)-performance slows-IOPS(input and output operation per second)-best redundancy 

~RAID 1-SLICING(HALF-HALF on each two disk)-best performance but low redundancy

~RAID 01-FIRST MIRRORING THEN SLICING(4 disk required) 

~RAID 10-FIRST SLICING THEN MIRRORING(4 disk required)

~RAID 5-(3 disk in which they sliced)-if one kill then data restored from the other two-widely accepted 

~RAID 6-(4 disk)

Raid configuration done on hardware (SAN)

17.EBS extended manually but EFS(ELASTIC FILE system) extended with the use and work only with LINUX.

18. DRV SOLUTION- MULTIPLE CLIENT ON SINGLE DISC
    
19. Amazon Relational Database Service (Amazon RDS)-a collection of managed services that makes it simple to set up,

operate, and scale databases in the cloud.

20. Amazon server -GLACIERS-a low-cost cloud storage service for data with longer retrieval times offered by Amazon Web

Services (AWS). Amazon Glacier provides storage for data archiving and backup of cold data.
    
21.HOW TO DEPLOY VPC

VPC,DOMAIN NAME , INTERNET, ROUTING(WHERE THE TRAFFIC GOES),DOPT,DSPT(DATA SECURITY PROTECTION TOOLKIT) OPTIONAL SET-BY
DEFAULT ATTACH BUT CAN BE REMOVED 

22.Note:why we need private IP if we have public IP ?

BECAUSE PUBLIC IP IS LIMITED AND WE SCALE THE PRIVATE IP.

~Private IP ranges-

•class A- 10.xxx

•class B- 172.16.x.x-172.13.x.x

•class C- 192.168.0.x

•class D- broadcast 

•class E- research 

23.DNS -URL into IP ADDRESS OR VICE VERSA

24.ROUTE 53-DNS WORK ON PORT NO. 53

25.DIRECT CONNECT-YOUR CONNECTION WITH AWS CONNECTION WITH WIRE- costly

## CLOUD COMPUTING KEYWORDS

1.bracket-QUANTUM COMPUTING

2.SNS(social networking services )-notification push(SMS)

3.SQS(QUEING SERVICE)

4.codebuild-build tools for compling ex: gradle,Apache ant

5.RDS(Amazon Relational Database Service (Amazon RDS))-

6.cloud trail-AWS CloudTrail is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account

7.code commit-manage service of git

8.code pipeling commit

9.CI/CD

DEPLOYMENT VS DILEVERED

10.CODE DEPLOYMENT

11.AWS COMPREHEND- SENTIMENT OR EMOTION ABOUT THE TEXT

12.AMAZON POLLY-TEXT TO SPOKEN WORD

13.AMAZON TRANSCRIBE- SPOKEN WORD TO TEXT

14.S3

  -it has durability99.99999999999%
  
 - globally unique bucket name
 - 
 - bucket policies
 - 
 - BUCKET ACLs-
 - 
 - OBJECT ACLs-
 
15.in-transit encryption- data is travel but cannot be read

16.at rest encryption- data is at rest but cannot be read until decrypt by private key 

17.s3 classes pic(27.50)

18.EC2 USES EBC AND INSTANCE STORE TO STORE DATA

DIFFERENCE BETWEEN EBC AND INSTANCE STORE

Instance store- faster and but at terminal data lost, temporary storage.

EBC INSTANCES-FEATURE OF BACKUP AND DATA will retain on until you delete 

19.EC2 instance type-

M type-GENERAL PURPOSE TO BALANCE MEMORY AND CPU

C type- MORE cpu 

T type- burst capilities -cheaper

R type -more RAM

D type-HUGE INSTANCE STORE

I type- IOPS PROVIDER

20.port number 

Ssh-22(linux)-ON UNSECURED NETWORK
 
Telnet-23

These all are TCP

BUT ROUTE 53

53-PORT NUMBER -UDP because it is fast and overhead .

21.RDP(REMOTE DESKTOP PROTOCOL)-MICROSOFT,USED FOR REMOTE(Windows)

22.three load balancer

Classic load balancer-layer 4 and 7

Application load balancer- layer 7

Use: support virtual host(use single web server to deploy different websites on path based )

Networking load balancer-layer 

Virtual hosting based on port no.

23.SSL WORK ON LAYER ON LAYER 7

Ssl v2 security attack heart bleed 

Ssl v3 version 3 came up and work on both layer 4 and 7

Note: web socket is not dealing with incryption

24.AUTOS SCALING-HA proxy 

Load balancer is used to for scaling so that ther is no much traffic 

25.security group-a firewall (control port base routing)


26.AMAZON LINUX(RED HAT)--> yum

    Ubuntu (Debian)--> apt-get


27.key

Public -username

Private-password


28.load balancer 

Use for scalability and control traffic

Use Round robin


29.Networking show availability zone

An availability zone consists of multiple data centers, which are all equipped with independent power, cooling and networking infrastructure all housed in separate facilities.


30.Netflix

Chaos Monkey is a software tool that was developed by Netflix engineers to test the resiliency and recoverability of their Amazon Web Services (AWS).


31.healthcheck 

Health checks are a way of asking a service on a particular server whether or not it is capable of performing work successfully.


32.Traffic port-load balancer get traffic


33.Override-when they are no traffic but wait for traffic 


provides options such as Virtual Waiting rooms that allow you to control how and when users can access your websites and applications.


34.4xx-client site error


      5xx-server site error 


      301/302-temporary redirection or                     permanent redirection


      200-working fine


35.cloud watch -by default it cannot give memory.That's why we use custom cloud watch 


36.Rabbit Q and SQS etc .these Q's help to scale.


37.prewarming-it for few resources like classic load balancer which cannot handle spike load so, we use in prewarm(means give it  artificial load)so, it at time need it scale.

This is called schedule scaling 


38.exit's IP-In private network , the traffic packets(peer-to-peer Mac address ) are connected by routering outside using route table


39.BGP-Border Gateway Protocol (BGP) refers to a gateway protocol that enables the internet to exchange routing information between autonomous systems (AS)


40.IGRP-In a host network, the Interior Gateway Routing Protocol (IGRP) is a proprietary distance vector routing protocol that is used to exchange routing information.


41.ARP-Address Resolution Protocol (ARP) is a protocol or procedure that connects an ever-changing Internet Protocol (IP) address to a fixed physical machine address, also known as a media access control (MAC) address, in a local-area network (LAN).


42.CLOUD WATCH - It use to alarm at the time of traffic by SMS,email etc 


43.API COMMUNICATE 

  a)pull based model- consumer pull according to convince


b)Pore based model - user pull at a certain time interval


C)event trigger -if one get trigger then other automatically trigger like lambda ,pipeline things.


44.Heath check 


Two types of health check


1.EC2 - The EC2 instance receives the request and performs its local health check logic.


2.ELB-The ELB sends a HTTP GET request to the /health path of the instance's web application.


45.VPC


TWO TYPES -

public/private 


46.subnets 


a)public-which can receive traffic from outside world 


b)private-which cannot  receive traffic and may or may not send to outside world


Subnet is public when we attach network gateway to it


Subnet is private when we cannot attach it with network gateway


47.NAT HAS ITS OWNS IP 


48. ROUTE TABLE -layer 7(Virtual)


49.if user hit the web server by chrome using public IP.


But if user want only consume internet it only stay in public network gateway


50.net instance or network gateway -act as source (send traffic outside) as well as distination (receiving the traffic)


51.neither source nor distination is called routing 


52. NAT-Receice traffic from private IP and send it to public 


53.miscreate table-Ip table of Linux as a full -fledged linux


54.NaCl(network access control list)-stateless (traffic come it may or may not be go)


55.subnets-statefull(traffic come but may default go out )


56.Transit gateway-A transit gateway is a network transit hub that you can use to interconnect your virtual private clouds (VPCs) and on-premises networks


57.CIDR-Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet


NOTE-BOTO library used in AWS use for python 


58.blue/green deployment (zero time deployment)-In software engineering, blue–green deployment is a method of installing changes to a web, app, or database server by swapping alternating production and staging servers


59.DDoS PROTECTION -DDoS mitigation refers to the process of successfully protecting a targeted server or network from a distributed denial-of-service (DDoS) attack


60.Aws buf-source IP occurance goes beyond threshold then it block it 


61. Yaml -use to create everything like security gp , many more instances 


62.RPO/RTO-These are the Recovery Time Objective (RTO) and Recovery Point Objective (RPO). RTO is the goal your organization sets for the maximum length of time it should take to restore normal operations following an outage or data loss. RPO is your goal for the maximum amount of data the organization can tolerate losing


63.CLOUD FORMATION -AWS CloudFormation is a service provided by Amazon Web Services that enables users to model and manage infrastructure resources in an automated and secure manner. Using CloudFormation, developers can define and provision AWS infrastructure resources using a JSON or YAML formatted Infrastructure as Code template
## how load balancer manage the traffic :
![Screenshot 2023-11-27 111333](https://github.com/Riyatomar14/keyword/assets/143107173/27fe9068-7b73-47d5-85ca-53571a7f2352)

![Screenshot 2023-11-27 111446](https://github.com/Riyatomar14/keyword/assets/143107173/a6cbbe9e-8436-4efc-baa2-f0bb48fb38de)






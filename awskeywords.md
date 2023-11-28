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

##CLOUD COMPUTING KEYWORDS
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
 - bucket policies
 - BUCKET ACLs-
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
Networking load balancer-layer 4
Virtual hosting based on port no.
23.SSL WORK ON LAYER ON LAYER 7
Ssl v2 security attack heart bleed 
Ssl v3 version 3 came up and work on both layer 4 and 7
Note: web socket is not dealing with incryption
24.AUTOS SCALING-HA proxy 
Load balancer is used to for scaling so that ther is no much traffic 
25.security group-a firewall (control port base routing)





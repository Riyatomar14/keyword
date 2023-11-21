1.Lambda-severless
2.Gartners magic quadrant -amazon is at at higher one 
3.Dedicated host -do not share with others 
4.Vendor lock in - use only one cloud and cannot shifted to other
5. private cloud -openstack,
open nebula , eucalyptus-in 2011
6.AWS beanstalk -for deploying and scaling web application
7.Paas-aws beanstalk
8.Saas-zoho cloud
9.labs as a service -in AWS 
10.BMC-base board management controller 
11.RKT or rocket-containation use
12.Database -(oracle-biggest player) - solution of golden gates -use multimaster solution where in AWS we use ARORA MASTER CLUSTER -
13.ECS-use dockerswarm in backend
EKS and ECS both cannot make server server less 
14.fargate over ECS/EKS-BACKND IS VANILLA or hardware.make the sever sever less.
15.S3(Amazon simple storage service)-
~Block storage-those can be formatted later time and attach with operating system.ex:elastic block store (EBS)-provide volume to EC2
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
19. Amazon Relational Database Service (Amazon RDS)-a collection of managed services that makes it simple to set up, operate, and scale databases in the cloud.
20. Amazon server -GLACIERS-a low-cost cloud storage service for data with longer retrieval times offered by Amazon Web Services (AWS). Amazon Glacier provides storage for data archiving and backup of cold data.
21.HOW TO DEPLOY VPC
VPC,DOMAIN NAME , INTERNET, ROUTING(WHERE THE TRAFFIC GOES),DOPT,DSPT(DATA SECURITY PROTECTION TOOLKIT) OPTIONAL SET-BY DEFAULT ATTACH BUT CAN BE REMOVED 
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

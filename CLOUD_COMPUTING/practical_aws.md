# Cloud Computing Practical

---

## 2. Launch Your First Amazon EC2 Instance
**Objective:** Deploy a virtual machine on AWS using Amazon EC2.

**a)** Launch an EC2 instance from the AWS Management Console.

**b)** Use a pre-configured AMI (e.g., Amazon Linux 2).

**c)** Configure security groups to allow SSH access.

**d)** Connect to the instance using SSH.

<img width="1324" height="654" alt="Screenshot 2026-04-16 160614" src="https://github.com/user-attachments/assets/0eacdc76-3c21-429f-a301-ecd53d18ca11" />

<img width="1917" height="947" alt="Screenshot 2026-04-16 154207" src="https://github.com/user-attachments/assets/c1bb9aa4-f57a-4d92-93c6-9b42e4b5dcc3" />

<img width="1903" height="953" alt="Screenshot 2026-04-16 154303" src="https://github.com/user-attachments/assets/ee47f2ea-53d1-4ebe-9c6c-1cdf327a60a3" />

<img width="1916" height="948" alt="Screenshot 2026-04-16 155625" src="https://github.com/user-attachments/assets/82c76d3a-6250-4f72-9c69-63ad38e759b8" />

## 3. Set Up a VPC
**Objective:** Create and configure a Virtual Private Cloud (VPC).

**a)** Create a custom VPC with a public and private subnet.

**b)** Launch an EC2 instance in the public subnet and another in the private subnet.

**c)** Configure an Internet Gateway for internet access in the public subnet.

**d)** Use a NAT Gateway to provide internet access for instances in the private subnet.
<img width="1915" height="957" alt="Screenshot 2026-04-16 162040" src="https://github.com/user-attachments/assets/1af60c5c-29df-4208-b847-e766d6d99c84" />
<img width="1913" height="962" alt="Screenshot 2026-04-16 162242" src="https://github.com/user-attachments/assets/a02a4b78-080e-4c7e-b6f8-b9c146008ff8" />
<img width="1918" height="954" alt="Screenshot 2026-04-16 162321" src="https://github.com/user-attachments/assets/76d3d753-5657-4899-aadc-e3692717b490" />
<img width="1916" height="952" alt="Screenshot 2026-04-16 162538" src="https://github.com/user-attachments/assets/76370243-e218-4291-a7ba-a79f366bfcd6" />
<img width="1915" height="957" alt="Screenshot 2026-04-16 162629" src="https://github.com/user-attachments/assets/f2e1afa2-ea26-409b-8b34-206c1f24627d" />
<img width="1918" height="957" alt="Screenshot 2026-04-16 162746" src="https://github.com/user-attachments/assets/e6aa5857-ea20-4678-87d1-1a281cb7a4aa" />
<img width="1917" height="955" alt="Screenshot 2026-04-16 162829" src="https://github.com/user-attachments/assets/129aabfa-5666-4a01-b4c6-a7c2e2e0ea54" />
<img width="1911" height="963" alt="Screenshot 2026-04-16 163006" src="https://github.com/user-attachments/assets/78b469e6-9de3-4503-be5e-0358d673bd7f" />
<img width="1912" height="957" alt="Screenshot 2026-04-16 163216" src="https://github.com/user-attachments/assets/87347cea-81f7-4d5d-b865-b12b7251c0e8" />
<img width="1904" height="959" alt="Screenshot 2026-04-16 164714" src="https://github.com/user-attachments/assets/de20f350-1b65-4a99-9aa2-3a634c7e267e" />
<img width="1907" height="962" alt="image" src="https://github.com/user-attachments/assets/99356fe2-f00b-47a6-b68b-058123ad850e" />
<img width="1919" height="993" alt="image" src="https://github.com/user-attachments/assets/656279a3-3d03-4694-9a41-d21f97d2ad54" />
<img width="1919" height="1079" alt="Screenshot 2026-04-16 172022" src="https://github.com/user-attachments/assets/ce44a87d-7b5e-4340-ae2a-ed187e3cdcf2" />
<img width="1918" height="1079" alt="Screenshot 2026-04-16 170519" src="https://github.com/user-attachments/assets/28a9fd4f-b25f-485f-92b7-c49c366fca92" />
<img width="1919" height="1077" alt="Screenshot 2026-04-16 172058" src="https://github.com/user-attachments/assets/c20ed219-71a6-44bd-a81a-c648f2962d00" />


## 4. Configure Auto Scaling and Load Balancing
**Objective:** Set up an auto-scaling group and load balancer.

**a)** Create an Auto Scaling Group and define a launch template.

**b)** Configure scaling policies (e.g., scale up when CPU utilization exceeds 70%).

**c)** Deploy an Application Load Balancer (ALB) to distribute traffic.

**d)** Test auto-scaling by simulating high traffic.


<img width="1903" height="953" alt="Screenshot 2026-04-16 173159" src="https://github.com/user-attachments/assets/c2c8935e-88f2-4754-bfc8-4bd67402c36e" />
<img width="1913" height="955" alt="Screenshot 2026-04-16 174601" src="https://github.com/user-attachments/assets/6a2867a3-078f-464d-b0b0-19310052aa41" />
<img width="1912" height="951" alt="Screenshot 2026-04-16 174720" src="https://github.com/user-attachments/assets/f5ba554c-6f7d-4860-933d-c75b5d98ce36" />
<img width="1912" height="956" alt="Screenshot 2026-04-16 174750" src="https://github.com/user-attachments/assets/7687e289-1d54-4c62-9c3f-3e495eda22f9" />
<img width="1916" height="961" alt="Screenshot 2026-04-16 173616" src="https://github.com/user-attachments/assets/14f7edb5-23de-484d-91a6-7197f231b705" />
<img width="1913" height="955" alt="Screenshot 2026-04-16 174229" src="https://github.com/user-attachments/assets/53c58dbb-b24f-4f0a-af9a-e1e6303deb9e" />
<img width="1902" height="962" alt="Screenshot 2026-04-16 174852" src="https://github.com/user-attachments/assets/75d396c0-dd44-4a5c-844a-0cac4a69594b" />
<img width="1911" height="955" alt="Screenshot 2026-04-16 175008" src="https://github.com/user-attachments/assets/16b2bc59-84eb-4083-9c70-7575230dbd98" />
<img width="1917" height="951" alt="Screenshot 2026-04-16 175120" src="https://github.com/user-attachments/assets/0c3e1b8f-0f69-4a55-9ec9-6bde344d30f1" />
<img width="1911" height="956" alt="Screenshot 2026-04-16 175246" src="https://github.com/user-attachments/assets/9afad869-8676-4fb0-a433-d7944609e071" />
<img width="1918" height="470" alt="Screenshot 2026-04-16 181003" src="https://github.com/user-attachments/assets/d34c03f3-2e6c-4e74-ac69-fbfdd501ae9d" />
<img width="1917" height="959" alt="Screenshot 2026-04-16 181251" src="https://github.com/user-attachments/assets/de1b9d6a-1167-4804-8933-9b2228d1b91a" />

## 5. Deploying a Static Website on the Cloud
**Objective:** Host a static website using cloud storage services.

**a)** Deploy a static website using any of the following:
- AWS S3
  
**b)** Configure permissions and enable public access.


<img width="1907" height="953" alt="Screenshot 2026-04-16 182823" src="https://github.com/user-attachments/assets/24edec84-3379-48d6-96e2-1aab2d68bebf" />
<img width="1908" height="950" alt="Screenshot 2026-04-16 182839" src="https://github.com/user-attachments/assets/b6cbe3d2-bfd2-45c9-afa1-6c4b31e8912f" />
<img width="1915" height="955" alt="Screenshot 2026-04-16 182909" src="https://github.com/user-attachments/assets/fbcdb847-e6ab-4de0-8040-6859b6b343b0" />
<img width="1911" height="944" alt="Screenshot 2026-04-16 182953" src="https://github.com/user-attachments/assets/650120ed-6868-482c-9f5c-34ea7689828a" />
<img width="1910" height="952" alt="Screenshot 2026-04-16 183027" src="https://github.com/user-attachments/assets/c5c82a6d-01d7-486e-bea4-976004a9981a" />
<img width="1917" height="1072" alt="Screenshot 2026-04-16 183112" src="https://github.com/user-attachments/assets/af54ec29-7b46-4cd9-a294-bcc3f6fbd696" />

## 6. Monitor Resources Using AWS CloudWatch
**Objective:** Use CloudWatch to monitor AWS resources.

**a)** Set up CloudWatch metrics for an EC2 instance (e.g., CPU utilization).

**b)** Create a CloudWatch Alarm to send notifications when a threshold is exceeded.

**c)** Configure an SNS topic for email notifications.

**d)** Test the setup by simulating high CPU usage.

<img width="1913" height="954" alt="Screenshot 2026-04-16 222811" src="https://github.com/user-attachments/assets/3f5b43fc-ec31-4bac-a26d-3e9b7f93c49e" />
<img width="1918" height="958" alt="Screenshot 2026-04-16 222906" src="https://github.com/user-attachments/assets/623fa630-28c5-423b-a86a-d07dd5a299e6" />
<img width="1907" height="947" alt="Screenshot 2026-04-16 223226" src="https://github.com/user-attachments/assets/1da43421-b5cf-480d-a6f5-187307e10cb0" />
<img width="8" height="6" alt="Screenshot 2026-04-16 223418" src="https://github.com/user-attachments/assets/6c49893e-ace9-4812-ad04-84987fd231be" />
<img width="1917" height="958" alt="Screenshot 2026-04-16 223445" src="https://github.com/user-attachments/assets/75633ae4-fd56-4510-b487-b8df4bc05bea" />
<img width="1915" height="948" alt="image" src="https://github.com/user-attachments/assets/60fa96bc-03ce-416c-84d1-3241b9a14df7" />

## 7. Install OpenStack
**Objective:** Set up a local OpenStack environment for practice.

<img width="1910" height="955" alt="image" src="https://github.com/user-attachments/assets/31b55e17-8032-429a-b3b7-8fea5e9ef440" />
<img width="1917" height="1079" alt="image" src="https://github.com/user-attachments/assets/16738c8f-e42e-435f-b236-960900c9a43a" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/464865eb-7cef-4152-834d-5786784d4690" />


## 8. Launch Your First OpenStack Instance
**Objective:** Create a virtual machine (VM) using OpenStack.

**a)** Create a project and assign roles to users.

**b)** Upload an image  to the Glance service.

**c)** Define a flavor to specify VM configurations.

**d)** Launch an instance using the Horizon dashboard or CLI.
<img width="1918" height="1077" alt="image" src="https://github.com/user-attachments/assets/38e76753-8ab8-4fd4-acc8-5f7cc07a2978" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/e8a34f57-08c0-4ad4-80c5-1cde250cec98" />
<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/b21c8537-3b2b-48a8-ba40-dfa0c7ffb56c" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ebb7f9f4-fdf2-4da4-aaa0-24c127c90c89" />
<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/f85bb5c8-22ff-45df-9268-a2870dce18c5" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/37ef6ff3-fe72-45a6-8072-40afbe9e3c43" />

## 9. Set Up Networking
**Objective:** Configure OpenStack Neutron to provide networking for instances.

**a)** Create a private network and a public network.

**b)** Attach a router to connect the private network to the public network.

**c)** Assign floating IPs to instances for external access.

<img width="1918" height="1079" alt="image" src="https://github.com/user-attachments/assets/3fccd920-cb1e-4a3d-8110-c3100dfdf59e" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0d13320a-5a80-44f8-81f7-47d95f7f7f08" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/8d1356a3-9d76-4a4a-8c95-e88bc8e3259e" />
<img width="1912" height="915" alt="Screenshot 2026-03-24 111436" src="https://github.com/user-attachments/assets/cdf99fe3-3df8-41d0-ab03-5c9dfc13509f" />
<img width="1916" height="918" alt="Screenshot 2026-03-24 111528" src="https://github.com/user-attachments/assets/d3d4825b-89a1-4c8a-a0f7-b5003b72d217" />




## 10. Cloud Security
**Objective:** Understand security practices in the cloud.

**a)** Implement IAM roles and policies for a cloud platform.

**b)** Create and assign least-privilege roles to users.

**c)** Configure data encryption for storage (e.g., S3 bucket encryption).

**d)** Set up a firewall rule and test its functionality.

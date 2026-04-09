# Cloud Computing Practical

---

## 2. Launch Your First Amazon EC2 Instance
**Objective:** Deploy a virtual machine on AWS using Amazon EC2.

**a)** Launch an EC2 instance from the AWS Management Console.

**b)** Use a pre-configured AMI (e.g., Amazon Linux 2).

**c)** Configure security groups to allow SSH access.

**d)** Connect to the instance using SSH.

<img width="668" height="640" alt="Screenshot 2026-03-24 093926" src="https://github.com/user-attachments/assets/3da560eb-e88f-472c-b13d-7ac569a59322" />
<img width="1907" height="777" alt="Screenshot 2026-03-24 093954" src="https://github.com/user-attachments/assets/e55a7116-406b-4c0c-825b-35336eb94fd3" />
<img width="1232" height="253" alt="Screenshot 2026-03-24 094003" src="https://github.com/user-attachments/assets/68183922-3efa-4f8a-95ad-349e8d77fb94" />
<img width="1224" height="418" alt="Screenshot 2026-03-24 094058" src="https://github.com/user-attachments/assets/7d89f0f2-441e-4a08-a32f-2ebc66de4d69" />
<img width="1915" height="858" alt="Screenshot 2026-03-24 094205" src="https://github.com/user-attachments/assets/6c6f1833-5334-4a2c-99ac-5c67dfb7af32" />
<img width="1913" height="878" alt="Screenshot 2026-03-24 094249" src="https://github.com/user-attachments/assets/e52855c6-a683-4f31-81f4-bde5d3441d36" />
<img width="1657" height="291" alt="Screenshot 2026-03-24 094400" src="https://github.com/user-attachments/assets/098367cd-439d-48a6-a787-ef5b1ebc8787" />

---

## 3. Set Up a VPC
**Objective:** Create and configure a Virtual Private Cloud (VPC).

**a)** Create a custom VPC with a public and private subnet.

**b)** Launch an EC2 instance in the public subnet and another in the private subnet.

**c)** Configure an Internet Gateway for internet access in the public subnet.

**d)** Use a NAT Gateway to provide internet access for instances in the private subnet.

<img width="1916" height="836" alt="Screenshot 2026-03-24 115314" src="https://github.com/user-attachments/assets/ff2c366c-0dc7-4593-bd49-37e492671930" />
<img width="1918" height="849" alt="Screenshot 2026-03-24 115333" src="https://github.com/user-attachments/assets/da767c98-2797-4276-af1d-c8e4e43b0e7b" />
<img width="1918" height="907" alt="Screenshot 2026-03-24 115351" src="https://github.com/user-attachments/assets/416d7d59-8378-47b2-be0c-aef4dcd1bc7e" />
<img width="1919" height="878" alt="Screenshot 2026-03-24 115428" src="https://github.com/user-attachments/assets/9b7aeac6-dfb6-4361-89cd-8346ebe8da0b" />
<img width="1919" height="890" alt="Screenshot 2026-03-24 115603" src="https://github.com/user-attachments/assets/f4ffb1cb-fa7b-4d99-9997-17bbf6ca0bde" />
<img width="1916" height="916" alt="Screenshot 2026-03-24 115706" src="https://github.com/user-attachments/assets/26a4dd3c-f285-4d92-bd87-bf05b1d1d137" />
<img width="1919" height="904" alt="Screenshot 2026-03-24 115722" src="https://github.com/user-attachments/assets/d1be5ac0-e496-40c1-9528-0929aba880a1" />
<img width="1919" height="778" alt="Screenshot 2026-03-24 115745" src="https://github.com/user-attachments/assets/3d95dac2-eeaa-4a78-904b-b54de0221357" />

---

## 4. Configure Auto Scaling and Load Balancing
**Objective:** Set up an auto-scaling group and load balancer.

**a)** Create an Auto Scaling Group and define a launch template.

**b)** Configure scaling policies (e.g., scale up when CPU utilization exceeds 70%).

**c)** Deploy an Application Load Balancer (ALB) to distribute traffic.

**d)** Test auto-scaling by simulating high traffic.

<img width="1918" height="876" alt="Screenshot 2026-03-24 121612" src="https://github.com/user-attachments/assets/1f920ee4-9b3a-469c-8781-257b35e8481d" />
<img width="1919" height="873" alt="Screenshot 2026-03-24 121659" src="https://github.com/user-attachments/assets/f4c09caf-e44d-4368-aefb-6bd2391740b9" />
<img width="1917" height="877" alt="Screenshot 2026-03-24 121711" src="https://github.com/user-attachments/assets/ba8a7551-76f9-4bd7-bbf7-27cef21a8e9c" />
<img width="1917" height="871" alt="Screenshot 2026-03-24 121907" src="https://github.com/user-attachments/assets/cc205457-8766-46e9-9cb7-53eaa5dbc656" />
<img width="1919" height="860" alt="Screenshot 2026-03-24 121955" src="https://github.com/user-attachments/assets/afc5c03e-88f9-4119-9cee-30abf5f42013" />
<img width="1919" height="871" alt="Screenshot 2026-03-24 122351" src="https://github.com/user-attachments/assets/7c39a3f3-6082-4ce2-8823-4523d6c6c204" />
<img width="1919" height="787" alt="Screenshot 2026-03-24 122416" src="https://github.com/user-attachments/assets/47e51530-039e-4f8b-9f00-2f3d285ea3a5" />
<img width="1919" height="751" alt="Screenshot 2026-03-24 122510" src="https://github.com/user-attachments/assets/ced1ea32-834e-421a-9bd4-2af8f9ae3a09" />


---

## 5. Deploying a Static Website on the Cloud
**Objective:** Host a static website using cloud storage services.

**a)** Deploy a static website using any of the following:
- AWS S3
  
**b)** Configure permissions and enable public access.

<img width="1919" height="911" alt="Screenshot 2026-03-24 112711" src="https://github.com/user-attachments/assets/4acbbefd-60f6-40b6-9b50-236876edc75c" />
<img width="1919" height="914" alt="Screenshot 2026-03-24 113142" src="https://github.com/user-attachments/assets/799a5e8d-6105-423a-b597-e7599516f27a" />
<img width="1918" height="870" alt="Screenshot 2026-03-24 113234" src="https://github.com/user-attachments/assets/7d73220c-e6e4-4bb7-b38f-fc0d0454f2a5" />
<img width="1916" height="978" alt="Screenshot 2026-03-24 112603" src="https://github.com/user-attachments/assets/ecba51ef-08a8-410a-aada-886ab6bfe4e1" />



---

## 6. Monitor Resources Using AWS CloudWatch
**Objective:** Use CloudWatch to monitor AWS resources.

**a)** Set up CloudWatch metrics for an EC2 instance (e.g., CPU utilization).

**b)** Create a CloudWatch Alarm to send notifications when a threshold is exceeded.

**c)** Configure an SNS topic for email notifications.

**d)** Test the setup by simulating high CPU usage.

<img width="1919" height="831" alt="Screenshot 2026-03-24 113905" src="https://github.com/user-attachments/assets/0c9d4afb-c743-4b9a-a617-a4f816672b44" />
<img width="1919" height="903" alt="Screenshot 2026-03-24 113942" src="https://github.com/user-attachments/assets/b823cb6c-9ffd-4c38-bc17-6564ccbf29f3" />
<img width="1917" height="837" alt="Screenshot 2026-03-24 113958" src="https://github.com/user-attachments/assets/c4ef5447-0202-4c0e-9820-5e49de503bc9" />
<img width="1918" height="838" alt="Screenshot 2026-03-24 114525" src="https://github.com/user-attachments/assets/2448345a-f8a2-4a88-9bfe-d4ed06e702bb" />
<img width="907" height="731" alt="image" src="https://github.com/user-attachments/assets/78402fc3-25a8-46ab-a9d7-902231885224" />
<img width="1919" height="839" alt="Screenshot 2026-03-24 114625" src="https://github.com/user-attachments/assets/6b35f46d-8633-4385-b0a3-93865f34ebc3" />


---

## 7. Install OpenStack
**Objective:** Set up a local OpenStack environment for practice.

<img width="1919" height="870" alt="Screenshot 2026-03-24 100410" src="https://github.com/user-attachments/assets/15335f49-3d0b-4476-b32d-4f149b80d49c" />
<img width="1918" height="974" alt="Screenshot 2026-03-24 100430" src="https://github.com/user-attachments/assets/bad29553-0c44-40d8-b264-7920078e5889" />
<img width="1919" height="966" alt="Screenshot 2026-03-24 100519" src="https://github.com/user-attachments/assets/adb8b135-383f-4dbd-97ce-5395f91b1efa" />

---

## 8. Launch Your First OpenStack Instance
**Objective:** Create a virtual machine (VM) using OpenStack.

**a)** Create a project and assign roles to users.

**b)** Upload an image  to the Glance service.

**c)** Define a flavor to specify VM configurations.

**d)** Launch an instance using the Horizon dashboard or CLI.

**a)**
<img width="913" height="619" alt="Screenshot 2026-03-24 101019" src="https://github.com/user-attachments/assets/c34d05ae-ac7e-44de-bce4-6b9237d09fca" />
<img width="1915" height="966" alt="Screenshot 2026-03-24 101034" src="https://github.com/user-attachments/assets/651f1d66-c9c7-445f-88c4-05c8815b3dea" />
<img width="1919" height="917" alt="Screenshot 2026-03-24 101245" src="https://github.com/user-attachments/assets/124394a2-1149-4982-bad0-44b04dcb08fa" />
<img width="1919" height="498" alt="Screenshot 2026-03-24 101314" src="https://github.com/user-attachments/assets/edaf4dc0-1920-4e94-931a-77d36b1be8d0" />
**b)**
<img width="1919" height="913" alt="Screenshot 2026-03-24 105038" src="https://github.com/user-attachments/assets/cb567f9c-4565-4ee8-89bf-78030cf21ff1" />
**c)**
<img width="978" height="900" alt="Screenshot 2026-03-24 101909" src="https://github.com/user-attachments/assets/8cbb507e-25ae-43b2-99f5-972ab17658cb" />
**d)**
<img width="1919" height="959" alt="Screenshot 2026-03-24 101939" src="https://github.com/user-attachments/assets/64e95e4c-53ea-4187-a466-6ad0156b3e2e" />

---

## 9. Set Up Networking
**Objective:** Configure OpenStack Neutron to provide networking for instances.

**a)** Create a private network and a public network.

**b)** Attach a router to connect the private network to the public network.

**c)** Assign floating IPs to instances for external access.

<img width="1916" height="914" alt="Screenshot 2026-03-24 111051" src="https://github.com/user-attachments/assets/7226c11a-615f-430d-a358-c062b0438838" />
<img width="1918" height="916" alt="Screenshot 2026-03-24 111103" src="https://github.com/user-attachments/assets/556b1eae-10bd-4402-96b1-8056287347c6" />
<img width="1916" height="922" alt="Screenshot 2026-03-24 111256" src="https://github.com/user-attachments/assets/8d38f5b4-fbde-434a-b8fd-98f6c4bc7258" />
<img width="1914" height="508" alt="Screenshot 2026-03-24 111419" src="https://github.com/user-attachments/assets/a1c3b3e6-e998-407c-97ea-0a1c6a16510b" />
<img width="1912" height="915" alt="Screenshot 2026-03-24 111436" src="https://github.com/user-attachments/assets/cdf99fe3-3df8-41d0-ab03-5c9dfc13509f" />
<img width="1916" height="918" alt="Screenshot 2026-03-24 111528" src="https://github.com/user-attachments/assets/d3d4825b-89a1-4c8a-a0f7-b5003b72d217" />

---

## 10. Cloud Security
**Objective:** Understand security practices in the cloud.

**a)** Implement IAM roles and policies for a cloud platform.

**b)** Create and assign least-privilege roles to users.

**c)** Configure data encryption for storage (e.g., S3 bucket encryption).

**d)** Set up a firewall rule and test its functionality.

<img width="1919" height="898" alt="Screenshot 2026-04-10 000414" src="https://github.com/user-attachments/assets/c0af7987-f058-4991-86d9-e318336930ee" />
<img width="1901" height="562" alt="Screenshot 2026-04-10 000615" src="https://github.com/user-attachments/assets/11343fd2-287b-41b6-8f6f-e2ab126e3867" />
<img width="1915" height="887" alt="Screenshot 2026-04-10 000744" src="https://github.com/user-attachments/assets/b3edec64-3b2f-4f1e-a4e9-f03b7014ddfd" />
<img width="1911" height="887" alt="Screenshot 2026-04-10 000810" src="https://github.com/user-attachments/assets/6aac97c2-9b20-4127-b561-7d69be1bf5b1" />
<img width="1912" height="892" alt="Screenshot 2026-04-10 001223" src="https://github.com/user-attachments/assets/0b9bb8fd-4a0c-4144-9040-fa2963c10202" />
<img width="1917" height="878" alt="Screenshot 2026-04-10 001255" src="https://github.com/user-attachments/assets/523912dc-1ecb-4ab5-8691-1c6e6414f5a5" />
<img width="1910" height="886" alt="Screenshot 2026-04-10 001849" src="https://github.com/user-attachments/assets/b3e0acb9-5a31-4d4c-8025-4c57c983159f" />
<img width="1915" height="885" alt="Screenshot 2026-04-10 002043" src="https://github.com/user-attachments/assets/a3583f9d-f3e4-4076-bbba-05c83d7be010" />


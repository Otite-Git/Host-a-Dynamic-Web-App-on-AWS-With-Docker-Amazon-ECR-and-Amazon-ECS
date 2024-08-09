Use of AWS to host a Dynamic Web App on AWS's leveraging Docker, Amazon ECR and Amazon ECS service suite.
# 💻Host a Dynamic Web App on AWS with Docker Amzon ECR and Amazon ECS☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken as a Cloud Engineer and Cloud architect enthusiast⚡️:

In this repository you will see a description of the project, low and high level architecture, scripting files and information on other key assets that I have used to develop this project as part of my portfolio and progressive development.

## **Website Page**

[www.rentzonepro.com](https://drive.google.com/file/d/1He_sJl0NVjHLmuV95Fla85G09DL8LAy0/view?usp=drive_link)

## **Project Overview** 

This project demonstrates how to host a Dynamic Web App on AWS, utilizing various AWS services for a scalable, secure, and highly available architecture. The key components include , creation of a Docker Hub account, 3-Tier AWs Network VPC, Nat Gateway 53, Security Groups, RDS Instances, Route 53, Bastion Host, SQL Scripting, IAM User Management and many more. The setup ensures high availability across multiple availability zones, security through security groups and SSL certificates, and scalability with auto-scaling groups.


![image](https://github.com/Otite-Git/Host-a-Dynamic-Web-App-on-AWS-With-Docker-Amzon-ECR-and-Amazon-ECS/assets/154989610/a6b60ad6-ba1c-4f5e-9255-c018bfdbb892)



- - - 
## **Architecture**

1. **Virtual Private Cloud (VPC):** Created a 3-Tier VPC with Public Subnets, Private App Subnets, and Private Data Subnets in 2 availability zones to segregate different components and enhance security.
2. **Public Subnets:** Used for infrastructure components like the NAT Gateway and Application Load Balancer.
3. **Internet Gateway:** Enables communication between instances in the VPC and the internet.
4. **Private Subnets:** Used to host the web server, designed to serve web pages and applications over the internet securely.
5. **EC2 Instances:** Utilized to host the WordPress website, accessible via an EC2 Instance Connect Endpoint.
6. **Bastion Host:** Used to migrate data into the RDS database whilst providing perimeter access and control security.
7. **AWS Fargate:** Helps to run containers without having to manage servers or clusters.
8. **S3 Bucket:** Enables environmental file storage.
9. **Application Load Balancer:** Distributes web traffic across an Auto Scaling Group of EC2 instances in two availability zones for high availability and fault tolerance.
10. **Availability Zones:** Ensures high availability and fault tolerance by deploying resources across multiple zones.
11. **Resources:** NAT Gateway, Bastion Host, and Application Load Balancer are deployed in Public Subnets.
12. **Auto Scaling Group:** Dynamically manages EC2 instances to ensure scalability, fault tolerance, and elasticity.
13. **Route 53:** Used for domain name registration and DNS record management.
14. **Docker:** Dockerfile created to build Docker image which will contain Build Arguments and Environment Variables to pass secrets to the Dockerfile. The Build Arguments allow us to build the image locally so it can be pushed to Amazon ECR. The Environment Variables are set to each Build Argument overall, eliminating the need to hard code sensitive information on the Dockerfile.
15. **Security Groups:** Acts as a network firewall to control traffic.
16. **Instances:** Configured to access the internet via the NAT Gateway, even in private subnets.
17. **GitHub:** Used for version control and collaboration, storing web files.
18. **Git:** Used to create a .gitignore file to prevent the Dockerfile from being committed to GitHub.
19. **Certificate Manager:** Manages SSL/TLS certificates to secure application communications.
20. **SNS:** Simple Notification Service is configured to alert about activities within the Auto Scaling Group.
21. **EFS:** Used for a shared file system.
22. **RDS:** Used for database management.
23. **IAM Roles:** Used to allow for the secret access key and access key ID to authenticate with AWS in order to push the container image to ECR.
24. **Flyway:** Used to organize scripts in the Flyway file which is then migrated securely via SSH Tunnel into the MySQL RDS.

## **Deployment Steps**

### VPC Setup
1. Create a VPC with public and private subnets across two availability zones. 
2. Enable DNS hostnames within the VPC.
3. Set up an Internet Gateway and attach it to the VPC. 
4. Create the public and private subnets for the availability zones, enabling auto-assign IP setting for the public subnets. 
5. Create a Route Table, add a route to direct network traffic to the Internet Gateway, and associate the two subnets with the route table. 
6. Create a NAT Gateway in the public subnet for internet access from private subnets.

### Security and Gateway Configuration
1. Configure security groups to allow necessary inbound and outbound traffic.
2. Set up Route 53 for domain name registration and DNS management.
3. Use AWS Certificate Manager to manage SSL/TLS certificates for secure communication.

### Script Configuration
1. Create a personal access token which Docker will use to clone the Application Code repository when the Docker image is built.
2. Create a folder in your Visual Studio Code which will host the following files, i.e., Dockerfile, AppServiceProvider.php (some files which you will create as a point in the project).
3. Build the Dockerfile that will be used to create the Docker image, updating the values and information within the Dockerfile script. (See the script below which is run using Visual Studio Code).
4. Create a replacement file for the AppServiceProvider.php in the folder you created. Enter the AppServiceProvider.php script below into the file. All of the required code is already in the root folder. We copy the file containing all the required code and replace it with the file in the application code. This is to ensure that the AppServiceProvider.php file contains the specific code set to redirect traffic from HTTP to HTTPS in order for the application to load properly.
5. As the file would contain sensitive information, rename Dockerfile to 'Dockerfile-reference' and create a .gitignore file for best practice. The Dockerfile-reference file should not be committed into a repository to ensure that any changes which are tracked and committed do not include the AppServiceProvider.php file as it contains sensitive information. Copy the 'Dockerfile-reference' file name into the .gitignore file. Note that the file was renamed to keep 'Dockerfile' available for the reference file which does not require sensitive information to be stored.
6. Create a new Dockerfile in the rentzone folder and copy the Dockerfile installation script below into the newly created Dockerfile. You'll see that this Dockerfile and the original Dockerfile (now titled Dockerfile-reference) look the same. The only difference is that the new Dockerfile contains Build Arguments and Environment Variables to pass secrets to the Dockerfile.
7. Write the script to build the Dockerfile image by creating a new file in the rentzone folder called build_image.sh. Copy the 'build_image.sh' script below into the build_image.sh file and for every build argument listed in the Dockerfile enter their values in the build_image.sh file.
8. The next step is to make the shell script file created above in line 7 executable. Using the command text script below, run 'chmod +x build_image.sh' in VS Code to execute the build_image.sh executable.
9. Run the shell script file to build the Docker image. Do this by right-clicking 'build_image.sh' and selecting 'open in integrated terminal.'

### Install AWS Command Line CLI
1. Visit www.docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
2. Depending on your OS, run the command line installer instructions on your terminal.

### IAM User Creation
1. Create an IAM user assigning administrative access. Create a secret access key and access key ID for the IAM user account. This is to allow for the secret access key and access key ID to authenticate with AWS in order to push the container image to ECR.
2. Run the AWS Configure Command on Command Prompt or Terminal and enter user access key ID and Secret Access Key information.

### ECR and Application Setup
1. Create a repository in Amazon ECR with AWS CLI using the command below:
    ```bash
    aws ecr create-repository --repository-name <repository-name> --region <region>
    ```
2. Push the Docker Image to the Amazon ECR repository already created by running the command below. Replace placeholders with the actual tag name and repository URI. In this case, the tag name used is `rentzone`. The repository URI can be located on the Amazon ECR repositories page. This command will re-tag the image, copy the image, and paste it with the terminal of the `rentzone` folder to successfully re-tag the image.
    ```bash
    docker tag <image-tag> <repository-uri>
    ```
3. Once the image is re-tagged, log into your Amazon ECR and run the command below to push the Docker Image into the Amazon ECR repository. Log into the management console to find the repository URI.
    ```bash
    docker push <repository-uri>
    ```
4. To log into Amazon ECR, use the script below updating the account ID and region information. This information can be obtained from the AWS management console. Once updated, copy and paste the command script in the open terminal of the `rentzone` folder.
    ```bash
    aws ecr get-login-password | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
    ```
5. Run the command to push the image into the ECR repository. Once this is completed, the ECS Fargate service will use this image to run the containers.
    ```bash
    docker push <repository-uri>
    ```

### Key Pair Creation
1. Create the Key Pair which will be used to SSH into the management instance.
2. Once you create your Key Pair, a note txt file will download containing the Key Pair information. Move this txt file to where your PowerShell terminal directory is pointing to. The reason for this is so when you run the command to SSH into the EC2 instance, the Key Pair will already be in the directory you run the SSH command from.

### Bastion Host Configuration
1. Create a Bastion Host Launch Instance using the Amazon Linux 2 AMI and T2 Micro, which are both free tiers.
2. Ensure to equip the Key Pair created above and select the VPC used to host the resources within the VPC environment.
3. Select the Public AZ1 Subnet and select the Bastion Host Security Group which you created in the Security Group creation step above.

### Flyway Configuration
1. Download Flyway Community Version and open the Flyway folder in Visual Studio Code.
2. Within the Flyway folder under 'conf', create a `flyway.conf` file.
3. In order to use Flyway to migrate data into the RDS MySQL Database, the Flyway configuration file must be updated with the credentials of the database as shown below:
    ```bash
    flyway.url=jdbc:mysql://localhost:3306/
    flyway.user=
    flyway.password=
    flyway.locations=filesystem:sql
    flyway.cleanDisabled=false
    ```

4. Copy the credential information above and past in into the newly created 'flyway.conf file created using your RDS configuration information i.e Master username and DB name to update the crednetials. This information will be used to connect the RDS Database.
5. Download and paste the SQL script to the SQL directory within the Flyway folder. The SQL script for the data that will be migrated into the RDS databse can be found under 'SQL Database Migration Script'
6. In order for Flyway to migrate the script into the RDS database,  Rename the SQL 'rentzone' file within the SQL folder to the format Flyway expects using the 'version__' method which is the name format Flyway expects.


### SSH Tunnel Setup 
1. In order to setup up SSH Tuunnel or Linux, Mac or Windows, the relevant command would need to be run. see directly below:
```bash
# to create an ssh tunnel in powershell, execute the following command:
ssh -i <key_pier.pem> ec2-user@<public-ip> -L 3306:<rds-endpoint>:3306 -N

# to create an ssh tunnel in linux or macOS, execute the following commands:
Note: Be sure to replace YOUR_EC2_KEY, LOCAL_PORT, RDS_ENDPOINT, REMOTE_PORT, EC2_USER, and EC2_HOST with your relevant information.

ssh -i "YOUR_EC2_KEY" -L LOCAL_PORT:RDS_ENDPOINT:REMOTE_PORT EC2_USER@EC2_HOST -N -f
```
Replace the generic parts of the command with the rlevant finromation partaining to your Key Pair Name, RDS Endpoint, local port number and the other information within the command you would need to replace.

2. Once you have filled in the command information, open a new terminal in VS Code and change your directory to where your Key Pair is stored paste the command within the terminal and press enter.
3. Once you press enter, open an integrated terminal to the flyway directory and run the Flway Migrate command below to migrate the data into the RDS database.
```bash
.\ flyway migrate
```

### Create the Application Load balancer
1. Prior to creating the Application Load Balancer, the Target Group must first be created to ensure that when the ECS Sevcie creates the tags, It will add those tags to the Target Group then the Application Load Balancer can route traffic to the tags in the target group.Ensure that when creating the Target Group IPv4 address type and HTTP at Port 80 is selected.
2. After the tags have been created, create the Applicaton Load Balancer within the VPC ensuring both Public Subnet AZ1 and AZ2 Availability Zones are selected as an Application Load Balancer always have to have a reach to the Public and not the Private Subnets. Under Security Group, remove the default seeting and select the Application Load Balancer security Group which was created.

### Certificate Manager
1. Register for a SSL Certificate from the AWS Certificate Manager which will be used to encrypt all communications between the web browser and web servers. Ensure to select 'DNS Validation' which is the method also recommended.
2. Once you request the certififcate, the status will state pending validation until a record set is created in Route 53 to validate the ownership of the domain names.

### HTTPS Listner Configuration
1. A HTTPS Listner will be created for the Application Load Balancer with the SSL Certficate created to the Listner to secure the communications between the ned users and the application.
2. Ensure that wen creating the HTTPS Listner the port number used is 443.

### Environment File Creation
1. Create an Environment File called' rentzone.env' to store the environment vairables defined in the Docker file. When the Docker file was created, the following variables below were defined within it:
```bash
PERSONAL_ACCESS_TOKEN=
GITHUB_USERNAME=
REPOSITORY_NAME=
WEB_FILE_ZIP=
WEB_FILE_UNZIP=
DOMAIN_NAME=
RDS_ENDPOINT=
RDS_DB_NAME=
RDS_MASTER_USERNAME=
RDS_DB_PASSWORD=
```
2. The 'build_image= script located within the Docker file will contain the this information which can be copy and pasted across to the 'rentzone.env' file. As this file constains sesnstive information, at the name ofthe file to the 'gitignore' file to ensure that the sensitvie information is not tracker and uploaded onto Git Hub.

### AWS S3 Bucket Creation
1. The S3 Bucket will be created to upload the environment file created in the step above. When the ECS Tags is created, it will retrieve the environment variables from the file in the S3 Bucket.
2. Ensure to create the S3 Bucket in the region where the VPC is hosted. Select the S3 Bucket that has been created and upload the environment file created in the step above into this S3 Bucket. The file to be uploaded for this project is titled 'rentzone.env'

### 2nd IAM User Creation
1. create and IAM Role to grant permission for ECS to execute tasks. The ECS Service will use the IAM role to access the environment file created above.
2. Select the Elastic Container Service as a Use Case for the IAM role and add two in line policies: to S3:GetObject and S3:GetBucketLocation. The inline policy will allow the ECS service to access the environment file uploaded into the S3 Bucket created above.

### ECS Cluster Creation
1. Create a Cluster assigning the VPC host environment to the Cluster. Assign Private App Subnet AZ1 and Private App Subnet AZ2 to the Subnet Selection.

### Task Definition Creation
1. Once the ECS Cluster is created, the Task Definition would be create which contains the blueprint and variables paremeters for a container e.g. the CPU and memory we would want to allocate to the container.
2. When creating the Task Definition, be sure to select the IAM role created for the purposes of Task Execution.
3. Once you have provided the name for the container, the image URI can be retrieve from the lastes Iamge within the ECR repository.
4. When configuring the environment variables, the environment file location can be retrieved from the ARN on the S3 bucket created above.
5. Depending on the Operation System used, select 'Linux/ARM64' if the image was build on a MAC computer. If the image was build on a MAC computer select 'Linux/X86_64.'
6. Under Task Execution Role, select the IAM role created which contains the in-line policy that will be ued to access the environment file in the S3 Bucket.

### ECS Service Creation
1. Creation of the ECs service which will create the Fargate containers. Selecter the exisitng cluster created. Ensure to select 'Use custom' and under Application Type select the Task Definition created above.
2. According to the reference architecture, there should be two desired tasks running so under the Desired tasks option specify two.
3. Under the Networking section, ensure the VPC host environemnt is selected and enable the Private App Subnet AZ1 and AZ2 as selected Subnet options
4. Select the existing Security Group created remvoing the default Secruity Group.
5. Turn off the Public IP settings as the container will be in a private subnet.
6. Under the Load Balancing section, the existing Application Load Balancer should be selected.
7. Select Port 80 HTTP as an exisitng Listner.
8. Under Target Group select an existing Target Group above.
9. Under Service Auto Scaling select one for when the Auto Scaling Group is scaling down the minimum number of tasks in relationt ohow many containers should be left.
10. For Maximum number of tasks, this is for when the containers are scaling upwards and how many containers it should scale to. For this enter 4.
11. Set a Policy name and set the Target Value, Scale-out cooldown period and Scale-in cooldown period to the figures provided.
12. Once the ECS Service has been created for this project, you should see after a few minutes the created rentzone servce. When it is selected, under the Health and metrics tab you should see 2 healthy tatgets running.

### Record Set Route 53 Creation
1. In order to see the application deployed on the Fargate Containers, a record set will be created in the ROute 53 hosted zone. Once the record set is created the end users will be able to use the created domain name to access the application deployed on the Fargate containers.
2. Within the Route 53 services Hosted zone terminal, selected the domain name, and set the record type to 'A - record type.' Also ensure to set the Record name to 'www'
3. route the traffic to 'Alias to Application and Classic Load Balancer.'
4. Select the region the Application Load Balancer was created in.
5. Select the Application Load Balancer.

## **How to Use**

1. Clone this repository to your local machine.
2. Follow the AWS documentation to create the required resources (VPC, subnets, Internet Gateway, etc.) as outlined in the architecture overview.
3. Use the provided scripts to set up the WordPress application on EC2 instances within the VPC.
4. Configure the Auto Scaling Group, Load Balancer, and other services as per the architecture.
5. Access the WordPress website through the Load Balancer's DNS name.

## **Additional Resources**

- **AWS Documentation:** Refer to the [AWS documentation](https://aws.amazon.com/documentation/) for detailed guides on setting up VPC, EC2, Auto Scaling, Load Balancer, and other services.
- **GitHub Repository Files:** Refer to [Otite-Git/Host-WorPress](https://github.com/Otite-Git/Host-a-WordPress-Website-on-AWS.git) to access the repository files for scripts, architectural diagrams, and configuration files necessary for deploying the website.

## **Contributing**

Contributions to this project are welcome! Please fork the repository and submit a pull request with your enhancements.

## **License**

This project is licensed under the MIT License - see the LICENSE file for details.

## **What problems did I solve by completing this project?**

1. **Scalability:** I was able to effectively Handle varying levels of web traffic efficiently through using AWS services like Auto Scaling and Elastic Load Balancing to automatically adjust the number of running instances based on traffic demand.
 
2. **Performance Optimisation:** I solved the problem of slow loading times and handling varying levels of web traffic effciently using AWS services like Auto Scaling and Elastic Load Balancing to automatically adjust the number of running instances based on traffic demand.

3. **Database Management:** Using AWS to host WordPress enabled me to effectively manage and optimise the database that supports WordPress through using Amazon RDS for managed MySQL a databases, enabling read replicas for load distribution.

4. **High Availability:** I Minimised downtime and ensuring continuous availability by deploying applications across 2 Availability Zones AZ1 & AZ2, using Elastic Load Balancing to distribute traffic, and setting up failover configurations.

5. **Cost Management:** I solved the problem of having high costs by supporting the deployment of a cost effective solution managing and optimising the costs associated with AWS resources. This was achieved through monitoring usage with AWS Cost Explorer, using AWS Budgets to set alerts, and leveraging Reserved Instances and Savings Plans for cost savings.

## **What issues did I face while working on the project and how did I resolve that issue?**
  
- **WordPress credentials issues:** I had faced the issue of my WordPress credentials automatically registering through an auto-fill feature generating a strong passsword which I did not record. I solved this issue by firstly deleting the existing EFS RDS and EC2 Instance and creating new EFS RDS and EC2 Instances. Once created, I then SSH'ed into the instance via Amazon Linux where I was to re-nstall the WordPress script which consisted of setting up the WordPress application on an EC2 instance, including Apache, PHP, MySQL, and mounting the Amazon EFS.

- **Increasing Costs:** The challenge of increasing cost also became a concern which I was able to resolve thorugh by firstly enabalbing MFA (Multi Factor Authentication) to enhance the security access of my root user account and enable best practice. Through this, I reduced the risk of fraudulent access to my account and using it resulting in high usage cost. Furthermore, I used AWS budgets and Cost Explorer to effectively manage costs by settting alerting and identifying which service was a high usage cost through visibility of the cost usage graph.  

 ## **What overall lessons did I learn?**
 
- **AWS Linux and Bash:** This project gave me the ability to increase my skills in AWS Linux and bash as I was required to use the EC2 Instance to install the WordPress script

- **Networking:** I further my knowledge on Networking through inplementation of tools such as the Internet Gateway. This enabled the resources within the VPC Public Subnet to connect to the internet, and resources within the VPC Private Subnet to connect to the internet via the NAT Gateway. The use of the NAT Gateway enables resources like the EC2 Instances on the Private App Subnet to access the internet and download package updates using 'Sudo Yum update' through SSH'ing into the EC2 instance. So there is a requirement for the EC2 Instance to have access to the internet without external users on the internet gaining access to the EC2 Instance.

- **IAM Management and Best Practice:** As part ot IAM Management best practice, I identified that it is not recommended to user a root account for cloud environment creation. Going forward, I increased the acess robustness of my root using account by regularly changing  passwords, using MFA (Mult Factor Authentication), removing access keys to the root account and reducing overall root user account user for sercurity perposes.

-  **Dockerfile Best Practice:** **- edited** Through doing this project, I also identified that going forward, best practice would be to create a Gitignore file to prevent the dockerfile being committed to Github restricting viewers who have access to the repository containing from viewing sensitive information such as personal access tokcen, Database endpoint usernames and password.

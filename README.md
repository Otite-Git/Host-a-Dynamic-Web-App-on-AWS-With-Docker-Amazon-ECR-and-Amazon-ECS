Use of AWS to host a Dynamic Web App on AWS's leveraging Docker, Amazon ECR and Amazon ECS service suite.
# 💻Host a Dynamic Web App on AWS with Docker Amzon ECR and Amazon ECS☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken as a Cloud Engineer and Cloud architect enthusiast⚡️:

In this repository you will see a description of the project, low and high level architecture, scripting files and information on other key assets that I have used to develop this project as part of my portfolio and progressive development.

## **WordPress Website Page**

[www.edit website name.com](https://drive.google.com/file/d/1Gy5ZhBRLFuDI_Mi-Fpw_jSVhp-mOQ7mo/view?usp=sharing)

## **Project Overview** - edited

This project demonstrates how to host a Dynamic Web App on AWS, utilizing various AWS services for a scalable, secure, and highly available architecture. The key components include , creation of a Docker Hub account, 3-Tier AWs Network VPC, Nat Gateway 53, Security Groups, RDS Instances, Route 53, Bastion Host, SQL Scripting, IAM User Management and many more. The setup ensures high availability across multiple availability zones, security through security groups and SSL certificates, and scalability with auto-scaling groups.


![image](https://github.com/Otite-Git/Host-a-Dynamic-Web-App-on-AWS-With-Docker-Amzon-ECR-and-Amazon-ECS/assets/154989610/a6b60ad6-ba1c-4f5e-9255-c018bfdbb892)



- - - 
## **Architecture**

1. **Virtual Private Cloud (VPC):** Created a 3 Tier VIPC with Public Subnets and Private App Subnets and Private Data Subnets in 2 availability zones to segregate different components and enhance security.
2. **Public Subnets:** Used for infrastructure components like the NAT Gateway and Application Load Balancer.
3. **Internet Gateway:** Enables communication between instances in the VPC and the internet.
4. **Private Subnets:** Used to host the web server, designed to serve web pages and applications over the internet securely.
5. **EC2 Instances:** Utilised to host the WordPress website, accessible via an EC2 Instance Connect Endpoint.
6. **Bastion Host:** Used to migrated data into the RDS database whiilst providing perimeter access and control security
7. **ECR Fargate:** Helps to run containers without having to manage servers or clusters.
9. **Application Load Balancer:** Distributes web traffic across an Auto Scaling Group of EC2 instances in two availability zones for high availability and fault tolerance.
10. **Availability Zones:** Ensures high availability and fault tolerance by deploying resources across multiple zones.
11. **Resources:** NAT Gateway, Bastion Host, and Application Load Balancer are deployed in Public Subnets.
12. **Auto Scaling Group:** Dynamically manages EC2 instances to ensure scalability, fault tolerance, and elasticity.
13. **Route 53:** Used for domain name registration and DNS record management.
15. **SSL:** Secures the website with an SSL certificate.
16. **Docker:** **- edited** Dockerfile created to build Docker image which will contains Build Arguments and Environment Variable to pass sercrets to the Dockerfile. The Build Argument allows us to build the image locally so it can be pushed to Amazon ECR. The Environemnt Variables are set to each Build Argument overall eliminating the need to hard code sensitive information on the Dockerfile.
17. **Security Groups:** Acts as a network firewall to control traffic.
18. **Instances:** Configured to access the internet via the NAT Gateway, even in private subnets.
19. **GitHub:** Used for version control and collaboration, storing web files.
20. **Git:** Used to create a Gitignore file to prevent the dockerfile being committed to Github.
21. **Certificate Manager:** Manages SSL/TLS certificates to secure application communications.
22. **SNS:** Simple Notification Service is configured to alert about activities within the Auto Scaling Group.
23. **EFS:** Used for a shared file system.
24. **RDS:** Used for database management.

## **Deployment Steps**

### VPC Setup 
1. Create a VPC with public and private subnets across two availability zones. **- edited**
2. Enable DNS Host names within the VPC. **- edited**
3. Set up Internet Gateway and attach it to the VPC. **- edited**
4. Create the Public and Private Subnets for the availability zones enabling auto assign IP setting for the public subnets. **- edited**
5. Create a Route Table and add a route to direct network traffic to the Intenet Gateway and associate the two subnets with the route table. **- edited**
7. Create a NAT Gateway in the public subnet for internet access from private subnets.

### Security and Gateway Configuration
1. Configure security groups to allow necessary inbound and outbound traffic.
2. Set up Route 53 for domain name registration and DNS management.
3. Use AWS Certificate Manager to manage SSL/TLS certificates for secure communication.

### EC2 and Application Setup
1. Launch EC2 instances in private subnets for hosting the WordPress application.
2. Set up Application Load Balancer in public subnets for distributing traffic.
3. Configure Auto Scaling Group for EC2 instances to ensure scalability.

### Script Confirugation
1. Create a personal access token which Docker will use to clone the Application Code repository when the Docker image is build.
2. Create a folder in your visual studio code which will host the following files i.e. Dockerfile, AppServiceProvider.php (some files which you will create as a point in the project).
3. Build the Dockerfile that will be used to create the docker image updating the values and information within the dockerfile script. (See the script below which is ran used Visual Studio Code).
4. Create a replacement file for the AppServiceProvider.php in the folder you created. Enter the AppServiceProvider.php script below into the file. All of the required code is already in the root folder. We copy the file containing all the required code and replace it with the file in the application code. This is to ensure that the AppServiceProvider.php has AppServiceProvider.php file contains the specific code set to redirect traffic from HTTP to HTTPs in order for the application to load properly.
5. As the file would contain sensitive information, rename Dockerfile to 'Dockerfile-reference' and create a Gitignore file for best practice. The Dockerfile-reference file should not be committed into a repository to ensure that any changes which are tracked and committed does not include the AppServiceProvider.php file as it is sensitive information. Copy the 'Dockerfile-reference' file name into the gitignore file. Note that the file was renamed to keep 'Dockerfile' available for the reference file which does not require sensitive information to be stored.
6. Create a new Dockerfile in the rentzone folder and copy the Dockerfile installation script below into the newly created Dockerfile. Youll see that this Dockefile and the orginal Dockerfile created now title Dockerfile-refence looks the same. The only difference is that the new Dockerfile contains Build Arguments and Environment Variable to pass sercrets to the Dockerfile.
7. Write the script to build the Dockerfile image by creating a new file in the renzone folder called build_image.sh. Copy the 'buid_image.sh script below into the buile_image.sh file and for every build argument listed in the Dockerfile enter their values in the build_image.sh file
8. The next step is to make the shell script file created above in line 7 executable. Using the command text script below run 'chmod +x build_image.sh' in VS Code to excute the build_image.sh executable.
9. Run the shell script file to build the Docker image. Do this right clicking 'build_image.sh and select 'open in integrated terminal.'

## **Install AWS Command Line CLI**
1. Visit www.docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
2. Depending on your OS, run the command line installer instructions on your terminal

## **IAM User Creation**
1. Create an IAM user assigning administrative access. Creatr an secret access key and access key ID for the IAM user account. This is to allow for the secret access key and access key ID to authenticate with AWS in order to push the container image to ECR.

## **README Structure**

- **Deployment Scripts:** Contains scripts for setting up opensource software LAMP stack (Linux, Apache, MySQL, PHP) used to build the Dynamic Web Application which is sripted within the Dockerfile and developed for the dockerimage. 
- **Architectural Diagrams:** Visual representation of the architecture and setup.
- **Configuration Files:** Includes files for configuring AWS resources and services.
- **Documentation:** Detailed documentation on setup, configuration, and usage.

## **Deployment Scripts**

### Dockerfile-reference Installation Script

This is script used to build the dockerfile image with sesntivie information inputted. This will be used a demonstration as to how to implement gitignore for the Dockerfile.

```bash
# Use the latest version of the Amazon Linux base image
FROM amazonlinux:2

# Update all installed packages to thier latest versions
RUN yum update -y 

# Install the unzip package, which we will use it to extract the web files from the zip folder
RUN yum install unzip -y

# Install wget package, which we will use it to download files from the internet 
RUN yum install -y wget

# Install Apache
RUN yum install -y httpd

# Install PHP and various extensions
RUN amazon-linux-extras enable php7.4 && \
  yum clean metadata && \
  yum install -y \
    php \
    php-common \
    php-pear \
    php-cgi \
    php-curl \
    php-mbstring \
    php-gd \
    php-mysqlnd \
    php-gettext \
    php-json \
    php-xml \
    php-fpm \
    php-intl \
    php-zip

# Download the MySQL repository package
RUN wget https://repo.mysql.com/mysql80-community-release-el7-3.noarch.rpm

# Import the GPG key for the MySQL repository
RUN rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022

# Install the MySQL repository package
RUN yum localinstall mysql80-community-release-el7-3.noarch.rpm -y

# Install the MySQL community server package
RUN yum install mysql-community-server -y

# Change directory to the html directory
WORKDIR /var/www/html

# Install Git
RUN yum install -y git

# Clone the GitHub repository
RUN git clone https://"your_personal_access_token"@github.com/"your_github_username"/"your_repository_name".git 

# Unzip the zip folder containing the web files
RUN unzip "your_repository_name"/"web_file_zip" -d "your_repository_name"/

# Copy the web files into the HTML directory
RUN cp -av "your_repository_name"/"web_file_unzip"/. /var/www/html

# Remove the repository we cloned
RUN rm -rf "your_repository_name"

# Enable the mod_rewrite setting in the httpd.conf file
RUN sed -i '/<Directory "\/var\/www\/html">/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf

# Give full access to the /var/www/html directory
RUN chmod -R 777 /var/www/html

# Give full access to the storage directory
RUN chmod -R 777 storage/

# Use the sed command to search the .env file for a line that starts with APP_ENV= and replace everything after the = character
RUN sed -i '/^APP_ENV=/ s/=.*$/=production/' .env

# Use the sed command to search the .env file for a line that starts with APP_URL= and replace everything after the = character
RUN sed -i '/^APP_URL=/ s/=.*$/=https:\/\/"your_domain_name"\//' .env

# Use the sed command to search the .env file for a line that starts with DB_HOST= and replace everything after the = character
RUN sed -i '/^DB_HOST=/ s/=.*$/="your_rds_endpoint"/' .env

# Use the sed command to search the .env file for a line that starts with DB_DATABASE= and replace everything after the = character
RUN sed -i '/^DB_DATABASE=/ s/=.*$/="your_rds_db_name"/' .env

# Use the sed command to search the .env file for a line that starts with DB_USERNAME= and replace everything after the = character
RUN sed -i '/^DB_USERNAME=/ s/=.*$/="your_rds_master_username"/' .env

# Use the sed command to search the .env file for a line that starts with DB_PASSWORD= and replace everything after the = character
RUN sed -i '/^DB_PASSWORD=/ s/=.*$/="your_rds_db_password"/' .env

# Copy the file, AppServiceProvider.php from the host file system into the container at the path app/Providers/AppServiceProvider.php
COPY AppServiceProvider.php app/Providers/AppServiceProvider.php

# Expose the default Apache and MySQL ports
EXPOSE 80 3306

# Start Apache and MySQL
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
```

### APPServiceProvider.php Script
```bash
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    /**
     * Bootstrap any application services.
     *
     * @return void
     */
    public function boot()
    {
        //set whatever level you want
        error_reporting(E_ALL ^ E_NOTICE);
    
        if (env('APP_ENV') === 'production') {
            \Illuminate\Support\Facades\URL::forceScheme('https');
        }
    }
    

    /**
     * Register any application services.
     *
     * @return void
     */
    public function register()
    {
        //
    }
}
```

### Dockerfile Installation Script

This script sets up the Dockerfile which will be used to build the Docker image contains Build Arguments and Environment Variable to pass sercrets to the Dockerfile eliminating the need to hard code sensitive information on the Dockerfile.


```bash
# Use the latest version of the Amazon Linux base image
FROM amazonlinux:2

# Update all installed packages to thier latest versions
RUN yum update -y 

# Install the unzip package, which we will use it to extract the web files from the zip folder
RUN yum install unzip -y

# Install wget package, which we will use it to download files from the internet 
RUN yum install -y wget

# Install Apache
RUN yum install -y httpd

# Install PHP and various extensions
RUN amazon-linux-extras enable php7.4 && \
  yum clean metadata && \
  yum install -y \
    php \
    php-common \
    php-pear \
    php-cgi \
    php-curl \
    php-mbstring \
    php-gd \
    php-mysqlnd \
    php-gettext \
    php-json \
    php-xml \
    php-fpm \
    php-intl \
    php-zip

# Download the MySQL repository package
RUN wget https://repo.mysql.com/mysql80-community-release-el7-3.noarch.rpm

# Import the GPG key for the MySQL repository
RUN rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023

# Install the MySQL repository package
RUN yum localinstall mysql80-community-release-el7-3.noarch.rpm -y

# Install the MySQL community server package
RUN yum install mysql-community-server -y

# Change directory to the html directory
WORKDIR /var/www/html

# Install Git
RUN yum install -y git

# Set the build argument directive
ARG PERSONAL_ACCESS_TOKEN
ARG GITHUB_USERNAME
ARG REPOSITORY_NAME
ARG WEB_FILE_ZIP
ARG WEB_FILE_UNZIP
ARG DOMAIN_NAME
ARG RDS_ENDPOINT
ARG RDS_DB_NAME
ARG RDS_MASTER_USERNAME
ARG RDS_DB_PASSWORD

# Use the build argument to set environment variables 
ENV PERSONAL_ACCESS_TOKEN=$PERSONAL_ACCESS_TOKEN
ENV GITHUB_USERNAME=$GITHUB_USERNAME
ENV REPOSITORY_NAME=$REPOSITORY_NAME
ENV WEB_FILE_ZIP=$WEB_FILE_ZIP
ENV WEB_FILE_UNZIP=$WEB_FILE_UNZIP
ENV DOMAIN_NAME=$DOMAIN_NAME
ENV RDS_ENDPOINT=$RDS_ENDPOINT
ENV RDS_DB_NAME=$RDS_DB_NAME
ENV RDS_MASTER_USERNAME=$RDS_MASTER_USERNAME
ENV RDS_DB_PASSWORD=$RDS_DB_PASSWORD

# Clone the GitHub repository
RUN git clone https://$PERSONAL_ACCESS_TOKEN@github.com/$GITHUB_USERNAME/$REPOSITORY_NAME.git

# Unzip the zip folder containing the web files
RUN unzip $REPOSITORY_NAME/$WEB_FILE_ZIP -d $REPOSITORY_NAME/

# Copy the web files into the HTML directory
RUN cp -av $REPOSITORY_NAME/$WEB_FILE_UNZIP/. /var/www/html

# Remove the repository we cloned
RUN rm -rf $REPOSITORY_NAME

# Enable the mod_rewrite setting in the httpd.conf file
RUN sed -i '/<Directory "\/var\/www\/html">/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf

# Give full access to the /var/www/html directory
RUN chmod -R 777 /var/www/html

# Give full access to the storage directory
RUN chmod -R 777 storage/

# Use the sed command to search the .env file for a line that starts with APP_ENV= and replace everything after the = character
RUN sed -i '/^APP_ENV=/ s/=.*$/=production/' .env

# Use the sed command to search the .env file for a line that starts with APP_URL= and replace everything after the = character
RUN sed -i "/^APP_URL=/ s/=.*$/=https:\/\/$DOMAIN_NAME\//" .env

# Use the sed command to search the .env file for a line that starts with DB_HOST= and replace everything after the = character
RUN sed -i "/^DB_HOST=/ s/=.*$/=$RDS_ENDPOINT/" .env

# Use the sed command to search the .env file for a line that starts with DB_DATABASE= and replace everything after the = character
RUN sed -i "/^DB_DATABASE=/ s/=.*$/=$RDS_DB_NAME/" .env 

# Use the sed command to search the .env file for a line that starts with DB_USERNAME= and replace everything after the = character
RUN  sed -i "/^DB_USERNAME=/ s/=.*$/=$RDS_MASTER_USERNAME/" .env

# Use the sed command to search the .env file for a line that starts with DB_PASSWORD= and replace everything after the = character
RUN  sed -i "/^DB_PASSWORD=/ s/=.*$/=$RDS_DB_PASSWORD/" .env

# Copy the file, AppServiceProvider.php from the host file system into the container at the path app/Providers/AppServiceProvider.php
COPY AppServiceProvider.php app/Providers/AppServiceProvider.php

# Expose the default Apache and MySQL ports
EXPOSE 80 3306

# Start Apache and MySQL
ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]t
```

### Script to build the Dockerimage Installation Script

Now that the Dockerfile has been created, the script below will be used to build the Dockerimage.

```bash
#!/bin/bash

# Run the docker build command
docker build \
--build-arg PERSONAL_ACCESS_TOKEN= \
--build-arg GITHUB_USERNAME= \
--build-arg REPOSITORY_NAME= \
--build-arg WEB_FILE_ZIP= \
--build-arg WEB_FILE_UNZIP= \
--build-arg DOMAIN_NAME= \
--build-arg RDS_ENDPOINT= \
--build-arg RDS_DB_NAME= \
--build-arg RDS_MASTER_USERNAME= \
--build-arg RDS_DB_PASSWORD= \
-t <image-tag> .
```
### Command script 

This command script contains the various script instructions to execute the buildimage.sh, execute the docker image and other intructions.

```bash
# make shell script executable: 
Set-ExecutionPolicy -ExecutionPolicy Unrestricted

# make shell script executable mac:
chmod +x build_image.sh

----------------------------------------------------------------

# aws cli command to create an amazon ecr repository
aws ecr create-repository --repository-name <repository-name> --region <region>
  
----------------------------------------------------------------

# retag docker image 
docker tag <image-tag> <repository-uri>

# login to ecr
aws ecr get-login-password | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com

# push docker image to ecr repository 
docker push <repository-uri>
  
----------------------------------------------------------------

# to create an ssh tunnel in powershell, execute the following command:
ssh -i <key_pier.pem> ec2-user@<public-ip> -L 3306:<rds-endpoint>:3306 -N


# to create an ssh tunnel in linux or macOS, execute the following commands:
Note: Be sure to replace YOUR_EC2_KEY, LOCAL_PORT, RDS_ENDPOINT, REMOTE_PORT, EC2_USER, and EC2_HOST with your relevant information.

ssh -i "YOUR_EC2_KEY" -L LOCAL_PORT:RDS_ENDPOINT:REMOTE_PORT EC2_USER@EC2_HOST -N -f
```

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

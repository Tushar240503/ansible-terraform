# ansible-terraform
 This project integrates Terraform and Ansible for AWS infrastructure automation, including VPC setup, EC2 provisioning, and Docker container deployment. It ensures security, scalability, and customization, streamlining the entire process for consistent infrastructure and application management in AWS.

This project seamlessly integrates Terraform and Ansible to automate the provisioning, configuration, and deployment of infrastructure resources in AWS while simultaneously managing Docker containers. It streamlines the entire process from setting up an AWS Virtual Private Cloud (VPC) to launching and configuring Docker containers, making it a powerful end-to-end infrastructure automation solution.

Infrastructure Provisioning with Terraform
The Terraform component of this project focuses on AWS resource provisioning and network setup:

AWS Configuration:

The project specifies the AWS region as "ap-south-1" for resource deployment.
Secure access is ensured by using AWS access and secret keys provided through variables.
AWS VPC:

Creates a custom VPC with a configurable CIDR block.
Tags the VPC with a customizable prefix for clear identification.
AWS Subnet:

Defines subnets within the VPC and associates them with specified availability zones.
Tags each subnet with a customizable prefix for easy management.
AWS Route Table and Internet Gateway:

Creates a custom route table and associates it with the VPC.
Adds a default route pointing to an internet gateway for external connectivity.
Tags the route table and internet gateway for better resource tracking.
AWS Security Group:

Establishes a security group with customizable inbound and outbound rules.
Allows SSH (port 22) and a specified application port (port 8080) from anywhere.
Ensures unrestricted outbound traffic.
Tags the security group for easy identification.
AWS Key Pair:

Generates an AWS key pair for secure SSH access to EC2 instances.
Utilizes the provided public key file for key generation.
AWS EC2 Instance:

Launches EC2 instances using the latest Amazon Linux 2 AMI.
Associates instances with specified subnets and security groups.
Provides public IP addresses for internet access.
Employs the generated AWS key pair for SSH authentication.
Executes a user-defined initialization script (entry-script.sh) during instance startup.
Tags instances for effective resource management.
Utilizes a local provisioner to run an Ansible playbook on instances for additional configuration.
Fine-Tuning with Ansible Playbooks
The Ansible component of this project fine-tunes the EC2 instances created by Terraform and deploys Docker containers:

Ansible Playbook 1: "Wait for SSH Connection"
Ensures SSH connectivity to instances.
Waits for SSH port 22 to become available.
Sets ansible_connection to "local" for local execution.
Ansible Playbook 2: "Install Python3, Docker, Docker-Compose"
Installs Python3 and Docker using the yum package manager.
Determines the Docker Compose download URL based on the host's architecture.
Installs Docker Compose.
Installs pip3, which is used to install Docker and Docker Compose.
Ensures compatibility with Python 3.
Ansible Playbook 3: "Add ec2-user to Docker Group"
Adds the ec2-user to the docker group, granting Docker management privileges.
Reconnects to the server session to apply group changes.
Ansible Playbooks 4 to 7: "Install Python Modules"
These playbooks install various Python modules (packaging, python-dotenv, docopt, texttable, and dockerpty) using pip3. They ensure the necessary Python dependencies are available for managing containerized applications.
Ansible Playbook 8: "Start Docker Containers"
Copies a Docker Compose YAML file to the Docker server.
Logs in to DockerHub using provided credentials.
Starts Docker containers defined in the Docker Compose file.
By combining Terraform and Ansible, this project provides a comprehensive infrastructure automation solution. It automates the setup of AWS resources, prepares EC2 instances with the required software and Python modules, and orchestrates Docker container deployments. This end-to-end automation ensures consistent and efficient infrastructure provisioning, configuration, and application deployment in AWS. Customization is made easy through variables and configuration files, allowing the project to adapt to different use cases and environments.
<img width="958" alt="Screenshot 2023-10-05 at 4 22 27 PM" src="https://github.com/Tushar240503/ansible-terraform/assets/98592305/6ea1818f-4a2a-45e2-a764-8da15c5e47bd">


<img width="989" alt="Screenshot 2023-10-06 at 5 55 02 PM" src="https://github.com/Tushar240503/ansible-terraform/assets/98592305/cadb85ad-008f-4395-82c8-a01bd3974438">


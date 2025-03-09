README File
Automated Deployment of a Web Application Using Terraform, Ansible, Docker, and GitHub Actions
Tools and Technologies Used
•	Terraform: For provisioning infrastructure on Azure.
•	Ansible: For automated server configuration.
•	Docker: For containerizing the web application.
•	GitHub Actions: For setting up a CI/CD pipeline to automate deployment.
Deployment Steps
Prerequisites
Ensure you have the following installed and configured:
•	An Azure account with appropriate permissions.
•	Terraform installed on your local machine.
•	Ansible installed on your local machine.
•	Git for version control.
•	Docker installed on your system.
Step 1: Terraform Setup
Navigate to the Terraform directory:
cd Terraform

Initialize Terraform:
terraform init

Review the execution plan:
terraform plan

Apply the configuration:
terraform apply -auto-approve

This will create the necessary cloud infrastructure on Azure.
Step 2: Ansible Configuration
Navigate to the Ansible directory:
cd ../Ansible

Edit the inventory file (inventory.ini) and replace <YOUR_VM_PUBLIC_IP> with your Azure VM’s actual public IP.
Run the playbook:
ansible-playbook -i inventory.ini playbook.yml

This will configure the server and deploy necessary dependencies.
Step 3: Docker Deployment
Build the Docker image:
docker build -t my-web-app .

Run the container:
docker run -d -p 80:80 my-web-app

Verify the Nginx server is running by accessing:
http://<YOUR_VM_PUBLIC_IP>

Step 4: CI/CD Pipeline with GitHub Actions
Set up a GitHub Actions workflow to automate the Docker container deployment.
1.	Commit and push changes to your GitHub repository.
2.	Ensure the GitHub Actions workflow is configured in .github/workflows/ci-cd-pipeline.yml.
3.	The workflow will: 
o	Build and push the Docker image to Azure Container Registry (if configured).
o	Deploy the container on the Azure VM.
o	Monitor pipeline execution in the GitHub Actions tab on GitHub.
Troubleshooting
•	Terraform issues: Ensure your Azure credentials are correctly configured in your environment variables.
•	Firewall rules: Confirm that your Azure VM allows HTTP traffic (port 80) in the security group.
•	Ansible playbook failures: 
o	Verify that the server IP and credentials are correct in inventory.ini.
o	Ensure SSH access to the Azure VM is properly configured.
•	Docker container not running: 
o	Run docker ps to check if the container is active.
o	If stopped, check logs with docker logs <container_id> to debug any errors.


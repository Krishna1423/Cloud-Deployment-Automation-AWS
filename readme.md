## Project Setup Instructions 

1. **Clone the Project Repository**
   - Begin by cloning the project repository.

2. **Create an S3 Bucket**
   - Before proceeding, create an Amazon S3 bucket. Remember to enable ACL and uncheck 'Block all public access'.

3. **Configure SSH Keys**
   - Navigate to the Terraform project directory and generate SSH keys for the `prod` environment:
     ```bash
     cd two-tier-web-application-automation-reflective-kangaroo/Terraform_Final/main
     ssh-keygen -t rsa -f bastion-reflective_kangaroo-prod
     ssh-keygen -t rsa -f reflective_kangaroo-prod
     ```

4. **Install Ansible**
   - Install Ansible by navigating to the Ansible directory and executing the following commands:
     ```bash
     cd ../../Ansible
     sudo yum install ansible -y
     pip2 install boto3 botocore
     ```

5. **Initialize and Apply Terraform in Backend**
   - Initialize and apply Terraform in the backend by moving to the backend directory:
     ```bash
     cd ../Terraform_Final/backend
     terraform init
     terraform apply -auto-approve
     ```

6. **Run Terraform in Main Project**
   - Navigate to the main Terraform folder and execute Terraform commands:
     ```bash
     cd ../main
     terraform init
     ```
   - It will ask for the bucket name while running terraform init, please put the name of the bucket you created and then run:
     ```bash
     terraform apply -auto-approve
     ```
   - Either copy and paste the link in the brower, or just copy it to be used later. 

7. **Run Ansible Playbook**
   - Return to the Ansible folder and run the playbook, replacing `<bucket_name>` with your created bucket name:
     ```bash
     cd ../../Ansible
     ansible-playbook -i aws_ec2.yaml Playbook.yaml -e "env=prod" -e "bucket=<bucket_name> "
     ```
   - Please rememeber if the playbook run on instance, or having another please try to run the playbook again without edit any code. (Just use upper allow key, and enter pr above code again)

8. **Accessing the Website**
   - Use the ALB DNS link (copied earlier) in a web browser (HTTP protocol). If you already did, just reload that page.

9. **Cleanup**
   - To clean up, navigate to the main and backend folders of Terraform_Final and destroy the resources:
     ```bash
     cd ../Terraform_Final/main
     terraform destroy -auto-approve
     ```

   - Wait for it to say
     ```bash 
     cd ../backend
     terraform destroy -auto-approve
     ```

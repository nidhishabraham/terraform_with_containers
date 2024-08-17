📝 Pre-requisite:

Create an AWS ECR Repository:

Name the repository: django-app.

Important: Replace 600735812827.dkr.ecr.us-west-1.amazonaws.com in the commands with your own ECR repository URL.

🔧 Steps:
1️) Update the VARIABLES.TF File:

Replace docker_image_url_django with your ECR repository URL.
2) Update IAM Policies:

Modify the policy file paths in both iam.tf and variables.tf files.
3) Log in to AWS ECR:

aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin <YOUR ECR REPO URL>

4) Navigate to the Application Directory:

cd app/

5) Build the Docker Image:

docker build -t <YOUR ECR REPO URL>/django-app:latest .

6) Build the Image for amd64 Platform:

docker build --platform=linux/amd64 -t <YOUR ECR REPO URL>/django-app:latest .

7) Push the Docker Image to ECR:

docker push <YOUR ECR REPO URL>/django-app:latest

8) Navigate to the Terraform Directory and Execute Commands:

Generate SSH Key Pair:

ssh-keygen -f california-region-key-pair

Initialize Terraform:

terraform init

Plan the Terraform Deployment:

terraform plan -out terraform.out

Apply the Terraform Plan:

terraform apply "terraform.out"

9) Install Required Python Packages:

pip install boto3 click

10) Set AWS Environment Variables:

export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION="us-west-1"

11) Deploy the Application:

Navigate to the deploy Folder:

cd deploy/

Run the Deployment Script:

python3 update-ecs.py --cluster=production-cluster --service=production-service

12) Clean Up Resources:

Destroy Terraform-managed Infrastructure:

terraform destroy
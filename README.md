## Overview
This repository contains the infrastructure and configuration code for the makeup lab. It uses Terraform to provision AWS resources and Ansible to configure Nginx web servers on Debian and Rocky Linux.

## 1. Generate SSH Keys
Run the following command locally to generate the SSH key pair:
```bash
ssh-keygen -t rsa -b 2048 -f ~/.ssh/makeup-key -q -N ""
```

## 2. Upload Key to AWS
The script in the scripts/ directory handles the upload of the public key to AWS.

```Bash

chmod +x scripts/import_lab_key
./scripts/import_lab_key keyname
```

## 3. Terraform Execution
Navigate to the terraform/ directory to provision the VPC, Subnets, Security Groups, and EC2 instances.

Initialize Terraform:

```Bash

cd terraform
terraform init
```

Format and Plan:

```Bash

terraform fmt
terraform plan -out=tfplan
```

Apply Infrastructure:

```Bash

terraform apply tfplan
Note the Public IPs outputted at the end of this step.
```

```Bash

cd ../ansible
ansible-playbook playbook.yml -i inventory
```

## 4. Validation & Screenshots

![alt text](image.png)
![alt text](image-1.png)

# Overview
This is an Ansible Tutorial with a Demo. We will use the following tools:
- **Terraform**: to provision the infrastructure
- **Ansible**: to configure the Jenkins application by creating the Jenkins container and configuring it
- **Docker**: to create the Jenkins container

## Run Terraform

Make sure you have your AWS credentials configured in your environment.

Let's create the infrastructure with the following command:

```bash
cd Terraform
terraform init
terraform apply -auto-approve
```

## Prepare the Ansible Inventory File

```bash
sed -i "s|<placeholder_app>|$(terraform output -raw public_ip)|g" ../Ansible/inventory
cat ../Ansible/inventory
```

## Prepare the SSH Key

```bash
terraform output -raw private_key > ../Ansible/myKey.pem
chmod 400 ../Ansible/myKey.pem
```

## Run Ansible

You can run the playbook with the following command:

```bash
cd ../Ansible
ansible-playbook --private-key myKey.pem -i inventory playbook.yaml
```
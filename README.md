# Overview
This is an Ansible Tutorial with a Demo. We will use the following tools:
- **Terraform**: to provision the infrastructure
- **Ansible**: to configure the Jenkins application by creating the Jenkins container and configuring it
- **Docker**: to create the Jenkins container

## Prepare the SSH Key

```bash
terraform output -raw private_key > /tmp/myKey.pem
chmod 400 /tmp/myKey.pem
```

## Prepare the Ansible Inventory File

```bash
sed -i "s/<placeholder_app>/$(terraform output -raw public_ip)/g" Ansible/inventory
cat Ansible/inventory
```

## Run Ansible

You can run the playbook with the following command:

```bash
cd Ansible && ansible-playbook --private-key /tmp/myKey.pem -i inventory jenkinsPlaybook.yaml
```
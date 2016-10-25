# Ansible Tower Demo Ops Resources
> Automation for the shared Ansible Tower demo server.

## Overview
This repo contains an Ansible project used to create and maintain a shared Ansible Tower demo environment. The idea is to handle automation of the following use

## Requirements
This project targets AWS for all demo resources. The following environment variables must be present in order to run any of the bootstrap playbooks:
- `ANSIBLE_AWS_ACCESS_KEY_ID`: The AWS_ACCESS_KEY_ID for the demo AWS account
- `ANSIBLE_AWS_SECRET_ACCESS_KEY`: The AWS_SECRET_ACCESS_KEY for the target AWS account
- `ANSIBLE_AWS_REGION`: The AWS_REGION for the target AWS account
- `TOWER_DEMO_KEYPAIR_NAME`: Name of the AWS keypair used to create the Tower server
- `ANSIBLE_AWS_PUBLIC_SUBNET_A_AZ`: Name of the AZ to map to public_subnet_a_az
- `ANSIBLE_AWS_PUBLIC_SUBNET_B_AZ`: Name of the AZ to map to public_subnet_b_az
- `ANSIBLE_AWS_PUBLIC_SUBNET_C_AZ`: Name of the AZ to map to public_subnet_c_az

One approach is to create an ```env.sh``` file and source it before running.

```
export ANSIBLE_AWS_ACCESS_KEY_ID=eggs
export ANSIBLE_AWS_SECRET_ACCESS_KEY=spam
export ANSIBLE_AWS_REGION=us-east-1
export TOWER_DEMO_KEYPAIR_NAME=key_name
export ANSIBLE_AWS_PUBLIC_SUBNET_A_AZ=us-east-1a
export ANSIBLE_AWS_PUBLIC_SUBNET_B_AZ=us-east-1d
export ANSIBLE_AWS_PUBLIC_SUBNET_C_AZ=us-east-1e
export ENVIRONMENT_NAME=ansible-demo
```

Note that your available AZs might be different than, literally, A, B, and C.

It is also necessary to have the following resources:
  - shared Ansible Vault passphrase

These values can be set in group_vars.

## Usage
```
ssh-agent bash
ssh-add /path/to/key_name.pem
source env.sh
ansible-playbook tower.yml --ask-vault-pass
```

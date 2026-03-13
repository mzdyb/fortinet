# Automating Fortinet Deployment on AWS with Ansible

This project automates the provisioning and deprovisioning of FortiGate and FortiManager instances on AWS using Ansible. It creates a complete lab environment including VPC networking, security groups, route tables and EC2 instances with multi-interface configurations.

## Architecture

The lab deploys the following infrastructure in AWS (`eu-central-1`):

- **VPC** (`10.0.0.0/16`) with an Internet Gateway
- **3 Subnets:**
  - `fntlab-subnet-public-mgmt` (10.0.0.0/24) — management and public access
  - `fntlab-subnet-private-lan1` (10.0.1.0/24) — private LAN 1
  - `fntlab-subnet-private-lan2` (10.0.2.0/24) — private LAN 2
- **FortiGate** (`t2.small`) — firewall with 3 network interfaces (1 public management + 2 private LANs), with an Elastic IP
- **FortiManager** (`m5.xlarge`) — centralized management appliance with 1 management interface and an Elastic IP
- **Route tables** configured so private subnets route traffic through FortiGate network interfaces

## Usage

### Deploy the lab

```bash
ansible-playbook -i inventory aws_deploy_fortinet_lab.yml
```

Or with Ansible Navigator:

```bash
ansible-navigator run aws_deploy_fortinet_lab.yml
```

### Remove the lab

```bash
ansible-playbook -i inventory aws_remove_fortinet_lab.yml
```

## Configuration

All infrastructure parameters are defined in `host_vars/aws`. This includes VPC CIDRs, subnet definitions, security group rules, network interface IPs, EC2 instance types, AMI IDs and route table configurations. Modify this file to customize the deployment.

# Setup and Configuration

## Prerequisites

- An AWS account and permissions to manage VPCs, Transit Gateways, route tables, security groups, and EC2 instances.
- An AWS Region selected for all resources. A Transit Gateway is regional, so the VPCs and attachments must be in the same Region for this setup.
- Three non-overlapping VPC CIDR blocks matching the ranges below.
- Review AWS pricing before creating resources; Transit Gateway attachments and running EC2 instances can incur charges.

This guide records the configuration and connectivity test for the project. It does not provision AWS resources automatically.

## 1. Create VPCs

Three VPCs were configured:

- DEV: 10.0.0.0/16
- STAGE: 20.0.0.0/16
- PROD: 30.0.0.0/16

## 2. Create Transit Gateway

A Transit Gateway was created to provide centralized connectivity between the three VPCs.

## 3. Create VPC Attachments

The following VPCs were attached to the Transit Gateway:

- VPC-DEV
- VPC-STAGE
- VPC-PROD

All three attachments reached the Associated state.

## 4. Configure Transit Gateway Routes

The Transit Gateway route table contains:

- 10.0.0.0/16
- 20.0.0.0/16
- 30.0.0.0/16

The routes were propagated from the VPC attachments.

## 5. Configure VPC Route Tables

Each VPC route table contains routes to the other VPC CIDR blocks through the Transit Gateway.

## 6. Configure Security Groups

ICMP traffic was permitted between the three VPC CIDR ranges for connectivity testing.

For production, avoid allowing unrestricted ICMP between entire VPC CIDR ranges unless that is explicitly required. Limit rules to the necessary sources and protocols, and remove temporary test rules when testing is complete.

## 7. Deploy EC2 Instances

One EC2 instance was deployed in each environment:

- EC2-DEV
- EC2-STAGE
- EC2-PROD

## 8. Test Connectivity

Connectivity was tested using ping between private IP addresses.

All tested connections returned:

4 packets transmitted, 4 received, 0% packet loss.

## 9. Contribute Changes

Create a feature branch with a name relevant to your change (replace the example name as needed):

```bash
git checkout -b feature/docs-guide
```

Review your changes and stage only the intended files before committing and pushing:

```bash
git status
git add docs/setup.md
git commit -m "Improve setup guide"
git push -u origin feature/docs-guide
```

Open a pull request from your feature branch into `main`. Do not push directly to `main`.
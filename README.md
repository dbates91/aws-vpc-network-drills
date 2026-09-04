# AWS VPC Network Drills

A hands-on AWS networking lab focused on repeatedly building, testing, breaking, and troubleshooting foundational AWS network environments.

## Project Goal

The goal of this project is to build a strong understanding of AWS networking fundamentals through repetition rather than memorization.

This lab starts with a simple public EC2 network and will gradually evolve into more advanced architectures, including private subnets and three-tier environments.

## Phase 1 — Public EC2 Networking Lab

### Architecture

Internet
↓
Internet Gateway
↓
Route Table
↓
Public Subnet
↓
Security Group
↓
EC2 Instance
↓
Apache Web Server

### AWS Services Used

* Amazon VPC
* Subnets
* Internet Gateway
* Route Tables
* Security Groups
* Amazon EC2

## Learning Objectives

By completing this lab repeatedly, I will practice:

* Creating a VPC from scratch
* Understanding CIDR ranges
* Creating and associating subnets
* Connecting a VPC to the internet
* Configuring route tables
* Understanding public IPv4 connectivity
* Configuring security groups
* Deploying an EC2 web server
* Troubleshooting broken network connectivity

## Lab Network

* VPC CIDR: `10.0.0.0/16`
* Public Subnet CIDR: `10.0.1.0/24`

### Internet Gateway

Created and attached an Internet Gateway named `network-drill-igw` to the VPC.

**Why:** The Internet Gateway provides the VPC with a connection point to the public internet. Attaching it alone does not make a subnet public; the subnet must also use a route table that sends internet-bound traffic to the Internet Gateway.

**Memory:** Internet Gateway = the VPC's entrance and exit to the internet.

### Public Route Table

Created a route table named `public-route-table` and associated it with `public-subnet-1`.

The route table contains:

* `10.0.0.0/16 → local`
* `0.0.0.0/0 → network-drill-igw`

**Why:** The route table determines where traffic from the subnet is sent. The local route allows communication within the VPC, while the default route sends internet-bound IPv4 traffic to the Internet Gateway.

**Key lesson:** A subnet becomes public because its associated route table contains a route to an Internet Gateway.

### EC2 Web Server

Launched an Amazon Linux 2023 EC2 instance named `network-drill-web` inside `public-subnet-1`.

The EC2 instance received a private IPv4 address from the `10.0.1.0/24` subnet and a public IPv4 address for internet connectivity.

**Why:** EC2 provides the actual workload inside the network. The VPC, subnet, routing, and security controls exist to provide controlled connectivity to resources such as this server.

**Key lesson:** A public IPv4 address alone does not make an EC2 instance publicly reachable. The subnet must also have a route to an Internet Gateway and the security group must permit the required traffic.

### Security Group

Created a security group for the EC2 web server with:

- SSH — TCP 22 — restricted to my public IP
- HTTP — TCP 80 — allowed from `0.0.0.0/0`

**Why:** The route table determines whether traffic has a network path. The security group determines whether that traffic is permitted to reach the EC2 instance.

**Security decision:** SSH was restricted to my IP rather than exposed to the entire internet.

### Apache Web Server

Installed Apache HTTP Server on the EC2 instance:

```bash
sudo dnf install httpd -y
sudo systemctl enable --now httpd
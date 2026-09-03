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

## Troubleshooting Exercises

This project will intentionally introduce networking failures such as:

* Missing security group rules
* Missing internet routes
* Incorrect route table associations
* Stopped web services
* EC2 connectivity problems

Each failure will be diagnosed, corrected, and documented.


# AWS EC2 – Web Server Deployment and Management Lab

## Project Overview
This hands-on lab covers provisioning and managing an Amazon EC2 instance, deploying an Apache web server with EC2 User Data, configuring HTTP access, monitoring instance health, resizing compute and storage resources, and testing termination protection.

## AWS Services and Concepts
- Amazon EC2
- Amazon EBS (gp3)
- Amazon VPC and subnet networking
- Security Groups
- Amazon CloudWatch monitoring
- Amazon Linux 2023
- Apache HTTP Server

## Implementation Steps

### 1. Launch an EC2 instance
- Launched an EC2 instance using Amazon Linux 2023.
- Selected the `t3.micro` instance type.
- Used the lab-provided VPC and security group.
- Enabled termination protection.
- Configured an 8 GiB root EBS volume.
- Proceeded without creating a key pair, as specified by the lab.

### 2. Deploy Apache using EC2 User Data
The following User Data script installs and starts Apache and creates a sample web page:

```bash
#!/bin/bash
yum -y install httpd
systemctl enable httpd
systemctl start httpd
echo '<html><h1>Hello From Your Web Server!</h1></html>' > /var/www/html/index.html
```

### 3. Configure HTTP access
- Configured the instance security group to allow inbound HTTP over TCP port 80 from `0.0.0.0/0`.
- Tested the web server using the instance's public IPv4 address over HTTP.
- Resolved an initial browser timeout and verified that the page loaded successfully.

> The lab website was accessed over HTTP (port 80); HTTPS was not configured.

### 4. Monitor the instance
- Reviewed EC2 status checks and CloudWatch monitoring metrics.
- Used the EC2 console to inspect instance health.

### 5. Resize compute and storage
- Changed the instance type from `t3.micro` to `t3.small`.
- Modified the attached gp3 EBS volume from 8 GiB to 10 GiB.
- Started the instance again and verified the updated configuration.

### 6. Test termination protection
- Attempted to terminate the instance while termination protection was enabled.
- Confirmed that AWS blocked the termination request.
- Disabled termination protection.
- Terminated the EC2 instance to complete the lifecycle exercise.

## Final Configuration

| Setting | Final lab configuration |
|---|---|
| AMI | Amazon Linux 2023 |
| Instance type | t3.small |
| vCPU | 2 |
| Memory | 2 GiB |
| Root EBS volume | gp3, 10 GiB |
| Web server | Apache HTTP Server |
| Inbound web access | HTTP, TCP 80 |
| Final instance state | Terminated |

## Key Learning Outcomes
- EC2 provisioning and lifecycle management
- Linux web server installation using User Data
- Security group configuration and HTTP connectivity troubleshooting
- EC2 health checks and CloudWatch monitoring
- EC2 instance type changes
- EBS volume modification
- Termination protection and safe instance cleanup

## Evidence
Add screenshots from your own lab session in a `screenshots/` directory, such as:
- EC2 instance running and status checks
- Successful Apache web page
- HTTP inbound security group rule
- CloudWatch monitoring view
- EBS volume showing 10 GiB
- Termination protection blocking a termination attempt
- Instance showing Terminated

Do not commit AWS credentials, private keys, temporary lab credentials, or sensitive account information.

## Environment
- Cloud provider: AWS
- Operating system: Amazon Linux 2023
- Web server: Apache HTTP Server
- Instance family: T3
- Block storage: Amazon EBS (gp3)

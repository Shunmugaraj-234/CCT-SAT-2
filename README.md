# 🛒 ShopKart – AWS Cloud Infrastructure

**A Scalable, Highly Available E-Commerce Web Application Using Amazon Web Services (AWS)**

## 📌 Project Overview

ShopKart is a cloud-based e-commerce application deployed on AWS. The project demonstrates how to distribute incoming web traffic across multiple EC2 instances, monitor server health, store files securely, and maintain application availability during server failures.

The infrastructure uses an Application Load Balancer, EC2 instances, a Target Group, Amazon S3, and Amazon CloudWatch.

## 🎯 Objectives

- Deploy the ShopKart web application on AWS EC2 instances.
- Distribute incoming requests across multiple servers.
- Monitor instance health using Target Group health checks.
- Maintain application availability when a server becomes unavailable.
- Store project files using Amazon S3.
- Monitor infrastructure metrics using Amazon CloudWatch.

## 🏗️ Architecture

```text
                   Users
                     |
                     v
          Application Load Balancer
                 (HTTP : 80)
                     |
                     v
             ShopKart Target Group
                /          \
               v            v
          Amazon EC2     Amazon EC2
          Server 1       Server 2
               \            /
                \          /
                 CloudWatch
                  Monitoring

              Amazon S3 Bucket
               File Storage
```

## ☁️ AWS Services Used

| AWS Service | Purpose |
|---|---|
| Amazon EC2 | Hosts the ShopKart web servers |
| Application Load Balancer | Distributes incoming HTTP requests |
| Target Group | Registers EC2 instances and performs health checks |
| Security Groups | Controls inbound and outbound network traffic |
| Amazon S3 | Stores project files and objects |
| Amazon CloudWatch | Monitors CPU utilization and infrastructure metrics |

## ⚙️ Implementation

### 1. Launch EC2 Instances

- Created two EC2 instances: `ShopKart-EC2-1` and `ShopKart-EC2-2`.
- Used Amazon Linux 2023.
- Installed and enabled the Apache HTTP Server.
- Created a ShopKart demo webpage on each instance.
- Configured HTTP access on port 80.

### 2. Configure the Target Group

- Created a target group named `ShopKart-TG`.
- Selected Instances as the target type.
- Configured HTTP on port 80.
- Set the health check path to `/`.
- Registered both EC2 instances.
- Verified that both targets reached the **Healthy** state.

### 3. Configure the Application Load Balancer

- Created an internet-facing Application Load Balancer named `ShopKart-ALB`.
- Configured the required Availability Zones and subnets.
- Configured HTTP listener traffic on port 80.
- Forwarded incoming requests to `ShopKart-TG`.
- Accessed the application using the ALB DNS name.

### 4. Verify Load Balancing

- Opened the ALB DNS URL in a browser.
- Refreshed the page multiple times.
- Verified that requests reached both EC2 servers by observing the different server labels.

### 5. Test Fault Tolerance

- Stopped one EC2 instance for the failure test.
- Verified that the load balancer stopped routing new requests to the unhealthy instance.
- Confirmed that the remaining healthy server continued serving requests.
- Restarted the stopped instance and verified its recovery.

### 6. Configure Amazon S3

- Created the bucket `shopkart-storage-2026-shanmugaraj`.
- Kept public access blocked.
- Created and uploaded `shopkart-product.txt`.
- Verified that the object appeared in the bucket.

### 7. Monitor with CloudWatch

- Opened CloudWatch Metrics.
- Selected EC2 CPU utilization metrics.
- Inspected infrastructure monitoring graphs.
- Configured a CPU utilization alarm with a threshold of 70% over a five-minute period.

## 🧪 Testing and Results

| Test Case | Expected Result | Status |
|---|---|---|
| EC2 deployment | Both web servers run successfully | Passed |
| Target health checks | Both targets become healthy | Passed |
| Load balancing | Requests reach both servers | Passed |
| Instance failure test | Traffic continues through the healthy server | Passed |
| S3 file upload | Sample object appears in the bucket | Passed |
| CloudWatch monitoring | EC2 metrics are available | Verified |

## 🔐 Security Considerations

- Used Security Groups to control network access.
- Kept S3 Block Public Access enabled.
- Used HTTP for this demonstration; production applications should use HTTPS.
- For production, restrict SSH access to trusted IP addresses and allow EC2 HTTP traffic from the ALB security group rather than the entire internet.
- Avoid storing credentials, access keys, or other secrets in the repository.

## 📚 Learning Outcomes

- Understanding AWS cloud infrastructure design.
- Deploying and configuring EC2 instances.
- Implementing load balancing and health checks.
- Testing fault tolerance and high availability.
- Managing objects using Amazon S3.
- Monitoring cloud resources using Amazon CloudWatch.

## 📄 Project Documentation

The practical documentation and implementation screenshots are available in:

**`ShopKart_AWS_Practical.pdf`**

Refer to the PDF for the detailed practical procedure and evidence.

## 🚀 Future Enhancements

- Configure Auto Scaling for automatic capacity adjustment.
- Add HTTPS using AWS Certificate Manager.
- Use Route 53 for custom domain routing.
- Configure CloudWatch alarms with Amazon SNS notifications.
- Integrate a database and a complete e-commerce backend.
- Deploy the application across multiple Availability Zones.

## 🏁 Conclusion

The ShopKart AWS cloud infrastructure was implemented using EC2, an Application Load Balancer, a Target Group, S3, Security Groups, and CloudWatch. Load balancing was verified, target health checks were successful, and a failure test demonstrated continued service through the healthy instance.

This project demonstrates the fundamentals of scalable, highly available, and monitored cloud application deployment.

---

**Project:** ShopKart – AWS Cloud Infrastructure  
**Domain:** Cloud Computing  
**Platform:** Amazon Web Services (AWS)  
**Application Server:** Apache HTTP Server  
**Protocol:** HTTP  
**Region:** US East (N. Virginia) — `us-east-1`

# Image Recognition Pipeline Using AWS Services
The objective of this project is to build an image recognition pipeline in Amazon Web Services (AWS) using Java applications running on two EC2 instances. The pipeline utilizes various AWS services such as Amazon S3 for storage, Amazon SQS for message queuing, and Amazon Rekognition for object and text recognition. The pipeline is designed to detect cars in images and perform text recognition on those images which contain cars.

This README provides instructions for setting up and running the image recognition pipeline using AWS services. The pipeline consists of two Java applications running on separate EC2 instances for car detection and text recognition, utilizing Amazon S3, SQS, and Rekognition.

## Table of Contents
1. [Architecture Overview](#architecture-overview)
2. [Setup Instructions](#setup-instructions)
3. [Execution Steps](#execution-steps)
4. [Monitoring and Troubleshooting](#monitoring-and-troubleshooting)
5. [Notes](#notes)

## Architecture Overview
The image recognition pipeline consists of the following components:
- Two EC2 instances (Instance A and Instance B)
- Amazon S3 bucket for storing images
- Amazon SQS for message queuing
- Amazon Rekognition for object and text recognition

Instance A detects cars in images and adds indexes of images with cars to SQS. Instance B processes these indexes, performs text recognition on corresponding images, and stores results.

## Setup Instructions
1. **Launch EC2 Instances:**
   - Launch two Amazon Linux EC2 instances (Instance A and Instance B) in the same VPC.
   - Configure Security Groups to allow inbound traffic on SSH, HTTP, and HTTPS ports from "MYIP".

2. **Install Java:**
   - Install Java on both instances.

3. **Copy Java Applications:**
   - Copy the Java applications for car detection and text recognition to their respective instances.

4. **Set Up AWS Credentials:**
   - Obtain AWS access key ID, secret access key, and session token.
   - Configure AWS credentials on both instances for accessing S3, SQS, and Rekognition services.

5. **Configure IAM Roles:**
   - Create IAM roles with appropriate permissions for EC2 instances to access AWS services securely.

6. **Configure SQS and S3:**
   - Create an SQS queue for message communication between instances.
   - Set up an S3 bucket for storing images.

## Execution Steps
1. **Run Instance A (Car Detection):**
   - Execute the Java application on Instance A.
   - Instance A reads images from the specified S3 bucket.
   - Detects cars in images using Rekognition.
   - Adds indexes of images with cars to SQS.

2. **Run Instance B (Text Recognition):**
   - Execute the Java application on Instance B.
   - Instance B reads indexes of images from SQS.
   - Downloads corresponding images from S3.
   - Performs text recognition using Rekognition on downloaded images.
   - Stores results in a file on associated EBS.

## Monitoring and Troubleshooting
- Monitor processing and results by checking log outputs from both instances.
- Use AWS CloudWatch for monitoring EC2 instances, SQS queue, and Rekognition service metrics.
- Troubleshoot any issues related to connectivity, permissions, or service configurations.

## Notes
- Ensure proper termination of EC2 instances after completing tasks to avoid unnecessary charges.
- Periodically refresh AWS credentials, especially in Educate accounts, to avoid session expiration.
- Follow AWS best practices for security, IAM roles, and resource management.


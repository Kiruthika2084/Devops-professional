## Table of contents
---
  * [Amazon-Inspector](#Amazon-Inspector)
  * [VPC-Endpoint](#VPC-Endpoint)
  
#### Amazon-Inspector
---
- assess network accessibility and security state of the applications run on those instances.
- produces a list of security findings organized by level of security.
- Can automate security assessment as part of development or deployment pipelines
- Also offers Agents which can be installed in EC2, which collects wide set of behaviour and configuration data.
- If recurring schedule of assessment is required,configure assessment template to run automatically by creating a lambda function.
- Alternatively, you can select the “Set up recurring assessment runs once every <number_of_days>, starting now” checkbox

#### VPC-Endpoint
---
- A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an Internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.
- There are two types of VPC endpoints: **interface endpoints and gateway endpoints**. You should create the type of VPC endpoint required by the supported service.
- If an IAM user has permission with s3:PutObject action on an Amazon Simple Storage Service (Amazon S3) bucket and got an HTTP 403: Access Denied error when uploading an object, then there might be an issue with the bucket or VPC endpoint policy.
- If the IAM user has the correct user permissions to upload to the bucket, then check the following policies for any settings that might be preventing the uploads:
  * IAM user permission to s3:PutObjectAcl
  * Conditions in the bucket policy
  * Access allowed by an Amazon Virtual Private Cloud (Amazon VPC) endpoint policy

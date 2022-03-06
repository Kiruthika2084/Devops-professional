## Table of contents
---
  * [Cloudwatch-Logs Subscription](#Cloudwatch-LogsSubscription)
  * [AWS-Config](#AWS-Config)
  * [HealthDashboard](#Healthdashboard)
  * [AWS-TrustedAdvisor](#AWS-TrustedAdvisor)
  * [Code-deploy](#Code-deploy)
  * [CloudTrail](#CloudTrail)
  
#### Cloudwatch-LogsSubscription
---
- Use Subscription for realtime feed of log events from cloudwatch logs.
- Can use Subsciption filter with Lambda, Kinesis and Kinesis Data Firehose.

#### AWS-Config
---
- Provides Visual Dahsboard to quickly spot non-complaint resources and take appropriate action.
- Notifies whenever resources are created, modified or deleted .
- AWS config rules can be used to evaluate the configuration settings of AWS resources.
- When AWS Config detects that a resource violates the conditions in one of your rules, AWS Config flags the resource as noncompliant and sends a notification.

#### HealthDashboard
---
##### AWS-HealthDashboard
- The service delivers alerts and notifications triggered by the changes in health of AWS resources
- Registered AWS users, with no setup can use the personal health Dashboard which is powered by AWS health API.
- AWS cloudwatch events can be used to detect and react to changes in PHD events. Only those specific to AWS account and resources.

##### Service-HealthDashboard
- Provides information about the regional availability of the service and not specific to AWS accounts, so not published to cloudwatch events.AWS-TrustedAdvisor

#### AWS-TrustedAdvisor
---

-  Trusted Advisor inspects your AWS environment, and then makes recommendations when opportunities exist to save money, improve system availability and performance, or help close security gaps. 
-  All AWS customers have access to *five* Trusted Advisor checks. 
-  Customers with a Business or Enterprise support plan can view all Trusted Advisor checks.
-  Can use *Amazon CloudWatch Events* to detect and react to changes in the status of Trusted Advisor checks. 
-  Use *Amazon CloudWatch* to create alarms on Trusted Advisor metrics for check status changes, resource status changes, and service limit utilization.

#### Code-deploy

- use Amazon CloudWatch Events to detect and react to changes in the state of an instance or a deployment (an “event”) in your CodeDeploy operations. 
- based on rules you create, CloudWatch Events will invoke one or more target actions when a deployment or instance enters the state you specify in a rule. 
- Depending on the type of state change, you might want to send notifications, capture state information, take corrective action, initiate events, or take other actions.
- You can select the following types of targets when using CloudWatch Events as part of your CodeDeploy operations:
    * AWS Lambda functions
    * Kinesis streams
    * Amazon SQS queues
    * Built-in targets (CloudWatch alarm actions)
    * Amazon SNS topics
 
 The following are some use cases:

  * Use a Lambda function to pass a notification to a Slack channel whenever deployments fail.
  * Push data about deployments or instances to a Kinesis stream to support comprehensive, real-time status monitoring.
  * Use CloudWatch alarm actions to automatically stop, terminate, reboot, or recover Amazon EC2 instances when a deployment or instance event you specify occurs.

#### CloudTrail

- **CloudTrail log file integrity validation** - To determine whether a log file was modified, deleted, or unchanged after CloudTrail delivered it
- When you enable log file integrity validation, CloudTrail creates a hash for every log file that it delivers.
- Every hour, CloudTrail also creates and delivers a file that references the log files for the last hour and contains a hash of each,called a digest file. 
- The digest files are put into a folder separate from the log files. 
- Each digest file also contains the digital signature of the previous digest file if one exists. 

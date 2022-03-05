## Table of contents
---
  * [Cloudwatch-Logs Subscription](#Cloudwatch-LogsSubscription)
  * [AWS-Config](#AWS-Config)
  * [HealthDashboard](#Healthdashboard)
  * [AWS-TrustedAdvisor](#AWS-TrustedAdvisor)
  
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

-  Trusted Advisor inspects your AWS environment, and then makes recommendations when opportunities exist to save money, improve system availability and performance, or help close security gaps. 
-  All AWS customers have access to *five* Trusted Advisor checks. 
-  Customers with a Business or Enterprise support plan can view all Trusted Advisor checks.
-  Can use *Amazon CloudWatch Events* to detect and react to changes in the status of Trusted Advisor checks. 
-  Use *Amazon CloudWatch* to create alarms on Trusted Advisor metrics for check status changes, resource status changes, and service limit utilization.



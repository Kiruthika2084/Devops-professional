---
## Table of contents
---
  * [CloudWatch-events](#CloudWatch-events)
  * [VPC](#VPC)
  * [S3-Events](#S3-Events)

### CloudWatch-events
---
- detect and react to changes in the status of Trusted Advisor checks. 
- based on the rules that you create, CloudWatch Events invokes one or more target actions when a check status changes to the value you specify in a rule. 
- targets when using CloudWatch Events as a part of your Trusted Advisor workflow:
  *  AWS Lambda functions
  *  Amazon Kinesis streams
  *  Amazon Simple Queue Service queues
  *  Built-in targets (CloudWatch alarm actions)
  *  Amazon Simple Notification Service topics
- no automatic checks on CloudWatch Events for AWS Trusted Advisor 

### VPC
---
-Amazon Virtual Private Cloud provides features that you can use to increase and monitor the security for your VPC
 * Security groups: Acts as firewall for associated EC2 instances, controlling both inbound and outbound traffic at instance level.
 * Network ACL:  act as a firewall for associated subnets, controlling both inbound and outbound traffic at the subnet level.
 * Flow logs: Flow logs capture information about the IP traffic going to and from network interfaces in your VPC. You can create a flow log for a VPC, subnet, or individual network interface. Flow log data is published to CloudWatch Logs or Amazon S3, and can help you diagnose overly restrictive or overly permissive security group and network ACL rules.
 * Traffic mirroring: You can copy network traffic from an elastic network interface of an Amazon EC2 instance. You can then send the traffic to out-of-band security and monitoring appliances
 * The default network ACL is configured to allow all traffic to flow in and out of the subnets with which it is associated.
 * Each network ACL also includes a rule whose rule number is an asterisk. This rule ensures that if a packet doesn’t match any of the other numbered rules, it’s denied.

### S3-Events
---
- When an event occurs in your account, CloudTrail evaluates whether the event matches the settings for your trails.
- Only events that match your trail settings are delivered to your Amazon S3 bucket and Amazon CloudWatch Logs log group.
- **Data events**: These events provide insight into the resource operations performed on or within a resource. These are also known as data plane operations.
- **Management events** - Management events provide insight into management operations that are performed on resources in your AWS account. 
   These are also known as control plane operations.
   Management events can also include non-API events that occur in your account. Captures login to console for example.
- You can configure multiple trails differently so that the trails process and log only the events that you specify. 
- Example, read only data and management events - seperate trail
- write only data and management events - seperate trail
- Data events are often high-volume activities.
  Example data events include:
    Amazon S3 object-level API activity (for example, GetObject, DeleteObject, and PutObject API operations)
    AWS Lambda function execution activity (the Invoke API)
- Data events are **disabled by default** when you create a trail. **


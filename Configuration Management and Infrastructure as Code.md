---
## Table of contents
---
* [Cloud-watch metrics<->CodeDeploy deployment group](#cloudwatch-metrics-codedeploy-deployment-group)
* [AWS-systems Manager](#AWS-systems-manager)
* [Cloud-Formation](#Cloud-Formation)
* [ECS<->Secrets](#ECS-Secrets)
* [AWS-Config](#AWS-Config)
* [VPC-endpoint](#VPC-endpoint)
* [Appspec-hooks](#Appspec-hooks)
* [codeDeploy-deploymentstrategies](#codeDeploy-deploymentstrategies)
* [ASG-ScheduledAction](#ASG-ScheduledAction)

 
#### cloudwatch-metrics<->CodeDeploy deployment group
---
- Create cloudwatch alarms for an instance or Amazon EC2 ASG in your codedeploy operations. 
- Alarm watches for metric and invoke actions when state changes.
- Can take actions like sending SNS, stopping, terminating or recovering an instance.
- Can configure to stop deployment when alarm is activated.
- **Can associate upto ten cloudwatch alarms with a codedeploy deployment group**
- If any of the alarms are activated, the deployment stops and the status is updated to stopped. 
  To use this option, grant Cloudwatch permissions to your codedeploy service role.

#### AWS-Systems-manager
---
- **Run command**- Remotely and securely manage the configuration of managed instances(machine in hybrid environment configured for systems manager)
- can use run command from console,cli, tool for powershell, sdk at no additional cost
- Administrators use run command for bootstrap,build deployment pipeline,configure log files, join instances to windows domain etc
- **parameter store** -store data such as passwords, licence codes, database strings as parameter values

##### To configure your hybrid servers and VMs for AWS Systems Manager
---
    1. Complete General Systems Manager Setup Steps
    2. Create an IAM Service Role for a Hybrid Environment
    3. Install a TLS certificate on On-Premises Servers and VMs
    4. Create a Managed-Instance Activation for a Hybrid Environment
    5. Install SSM Agent for a Hybrid Environment (Windows)
    6. Install SSM Agent for a Hybrid Environment (Linux)
    7. (Optional) Enable the Advanced-Instances Tier
- Create a consistent and secure way to remotely manage your hybrid workloads from one location using the same tools or scripts.
- After you finish configuring your servers and VMs for Systems Manager, your hybrid machines are listed in the Console and described as managed instances.
- The IDs of your hybrid instances are distinguished from Amazon EC2 instances with the prefix “mi-“. Amazon EC2 instance IDs use the prefix “i-“.
- Servers and virtual machines (VMs) in a hybrid environment require an IAM role to communicate with the Systems Manager service. The role grants 

#### Cloud-Formation
---
- Cross stack references to export resources from one stack to another
- Stacks can use the exported resources by calling them using Fn:ImportValue function
- Use seperate stacks to create related AWS resources
- ![image](https://user-images.githubusercontent.com/81581601/156093802-0ff739f1-3715-4f2a-929a-46aa16b3539d.png)

##### stack
---
- A stack is a collection of AWS resources that you can manage as a single unit.
- can create, update, or delete a collection of resources by creating, updating, or deleting stacks. 
- If you no longer require that web application, you can simply delete the stack, and all of its related resources are deleted.
- If a resource cannot be deleted, any remaining resources are retained until the stack can be successfully deleted.
- create a nested stack within another stack by using the AWS::CloudFormation::Stack resource.
- As your infrastructure grows, common patterns can emerge in which you declare the same components in multiple templates. You can separate out these common components and create dedicated templates for them. Then use the resource in your template to reference other templates, creating nested stacks.
- By setting up both the MinSize and MaxSize parameters of the Auto Scaling group to 1, you can ensure that your EC2 instance can recover again in the event of systems failure with exactly the same parameters defined in the CloudFormation template.This is one of the Auto Scaling strategies which provides high availability with the least possible cost. In this scenario, there is no mention about the scalability of the solution but only its availability.

##### custom-resource
---
- Include resources that are not cloudformation resource types, using custom-resource. Write custom provisioning logic in templates that AWS cloudformation runs anytime you update,create or delete stacks.This way we can manage all related resources in a single stack.
- Use the AWS::CloudFormation::CustomResource or alternatively, the Custom::<User-Defined Resource Name> resource type to define custome resources in templates
- custom resources require one property ,service token which specifies where CF sends requests, such as SNS
- Associating Lambda with custome resources, the functions is invoked whenever custom resource is created, modified or deleted. CF calls Lambda API and pass request data to the function.
- The power and customizability of Lambda functions in combination with AWS CloudFormation enable a wide range of scenarios, such as dynamically looking up AMI IDs during stack creation, or implementing and using utility functions, such as string reversal functions.
- Normally, you might map AMI IDs to specific instance types and regions. To update the IDs, you manually change them in each of your templates. By using custom resources and AWS Lambda (Lambda), you can create a function that gets the IDs of the latest AMIs for the region and instance type that you’re using so that you don’t have to maintain mappings.
- cfn-init helper script is primarily used to fetch metadata, install packages and start/stop services to your EC2 instances that are already running. 


#### ECS<->Secrets
 ---
- ECS enables to inject sensitive data in container either by storing in Secrets manager or parameter store, and then referencing them in container definition.
- In container definition, specify **secrets** with the name of environment variable and full ARN of the secret parameter.
- The parameter referenced can be in the different region, but same account.
- Secrets Manager - dedicated secrets store with lifecycle management
- parameter Store - Single store for configuration and secrets.
 
 #### AWS-Config
 ---
 - AWS Config provides a detailed view of the configuration of AWS resources in your AWS account. 
 - how the resources are related to one another and how they were configured in the past to see how the configurations and relationships change over time.
 - AWS Config evaluates your resource configurations against the rule when the trigger occurs.
 - There are two types of triggers:
   *Configuration changes
   *Periodic

 
 
 #### VPC-endpoint
 ---
 - VPC endpoint enables to privately connect AWS resources and VPC endpoint services.
 - Types of endpoints: Interface endpoints and gateway endpoints(S3 & dynamoDB) 
 
 #### Appspec-hooks
 ----
 
 - The content in the 'hooks' section of the AppSpec file varies, depending on the compute platform for your deployment.
 - The 'hooks' section for an EC2/On-Premises deployment contains mappings that link deployment lifecycle event hooks to one or more scripts. 
 - he 'hooks' section for a Lambda or an Amazon ECS deployment specifies Lambda validation functions to run during a deployment lifecycle event. 
 - If an event hook is not present, no operation is executed for that event.
 - During each deployment lifecycle event, hook scripts can access the following environment variables:
   *  APPLICATION_NAME
   *  DEPLOYMENT_ID 
   *  DEPLOYMENT_GROUP_NAME 
   *  DEPLOYMENT_GROUP_ID
   *  LIFECYCLE_EVENT
  - These environment variables are local to each deployment lifecycle event.

 
#### codeDeploy-deploymentstrategies
 -----
 
 - When you deploy to an AWS Lambda compute platform, There are three ways traffic can shift during a deployment:
   * Canary : Traffic is shifted in two increments
   * Linear :Traffic is shifted in equal increments with an equal number of minutes between each increment.
   * All-at-once : All traffic is shifted from the original Lambda function to the updated Lambda function version all at once.
 
 #### ASG-ScheduledAction
 ----
 
 - To configure your Auto Scaling group to scale based on a schedule, you create a scheduled action.
 - At the specified time, Amazon EC2 Auto Scaling updates the group with the values for minimum, maximum, and desired size specified by the scaling action.
 - can create scheduled actions for scaling one time only or for scaling on a recurring schedule.
 

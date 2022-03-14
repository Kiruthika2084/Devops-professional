---
## Table of contents
---
* [CodeCommit](#CodeCommit)
* [AWS-managed-policies](#awsmanaged-policies)
* [AutoScalingGroup-UpdatePolicy](#ASG-UpdatePolicy)
* [CloudFormation-Lifecycle hooks](#CloudFormation-Lifecyclehooks)
* [AWS-CodePipeline](#AWS-CodePipeline)
* [Lifecycle-Hook](#Lifecycle-Hook)
* [ECS](#ECS)
* [SSM](#SSM)


### CodeCommit
---

- A repository is the fundamental version control object in CodeCommit. 
- If you add AWS tags to repositories, you can set up notifications so that repository users receive email about events (for ex, another user commenting on code).
- You can create triggers for your repository so that code pushes or other events trigger actions, such as emails or code functions. 
- You can even configure a repository on your local computer (a local repo) to push your changes to more than one repository.

### 'AWSmanaged-policies'
---

#### AWSCodeCommitFullAccess 
– Grants full access to CodeCommit. 

#### AWSCodeCommitPowerUser 
– Allows users access to all of the functionality of CodeCommit and repository-related resources,
except it does not allow them to delete CodeCommit repositories or create or delete repository-related resources in other AWS services,
such as Amazon CloudWatch Events. It is recommended to apply this policy to most users.

#### AWSCodeCommitReadOnly 
– Grants read-only access to CodeCommit and repository-related resources in other AWS services.


We cannot modify AWS-managed policies. In order to customize, we can add a Deny rule to block some capabilities included in these policies.


### 'ASG-UpdatePolicy'
---

#### AWS CloudFormation replacement updates– AutoScalingReplacingUpdate policy. 

AWS::AutoScaling::AutoScalingGroup resource type reference in your CloudFormation template to define an Amazon EC2 Auto Scaling group with the specified name and attributes. To configure Amazon EC2 instances launched as part of the group, you can specify a launch template(better with new features) or a launch configuration.

You can add an **UpdatePolicy attribute to your Auto Scaling group to perform rolling updates (or replace the group)** when a change has been made to the group.

**AutoScalingReplacingUpdate policy** will create a separate Auto Scaling group and is able to perform an immediate rollback of the stack in an event of an update failure.

During replacement, AWS CloudFormation retains the old group until it finishes creating the new one. If the update fails, AWS CloudFormation can roll back to the old Auto Scaling group and delete the new Auto Scaling group. While AWS CloudFormation creates the new group, it doesn’t detach or attach any instances. After successfully creating the new Auto Scaling group, AWS CloudFormation deletes the old Auto Scaling group during the cleanup process.

```
UpdatePolicy:
  AutoScalingReplacingUpdate:
    WillReplace: Boolean
```
When you set the WillReplace parameter, remember to specify a matching CreationPolicy. If the minimum number of instances (specified by the MinSuccessfulInstancesPercent property) don’t signal success within the Timeout period (specified in the CreationPolicy policy), the replacement update fails and AWS CloudFormation rolls back to the old Auto Scaling group.


**AutoScalingRollingUpdate policy** controls how AWS CloudFormation handles rolling updates for an Auto Scaling group. This common approach keeps the same Auto Scaling group, and then replaces the old instances based on the parameters that you set.

The AutoScalingRollingUpdate policy supports the following configuration options:
```
"UpdatePolicy": {
  "AutoScalingRollingUpdate": {
    "MaxBatchSize": Integer,
    "MinInstancesInService": Integer,
    "MinSuccessfulInstancesPercent": Integer,
    "PauseTime": String,
    "SuspendProcesses": [ List of processes ],
    "WaitOnResourceSignals": Boolean
  }
}
```

**If both the AutoScalingReplacingUpdate and AutoScalingRollingUpdate policies are specified, setting the WillReplace property to true gives AutoScalingReplacingUpdate precedence. But since this property is set to false, then the AutoScalingRollingUpdate policy will take precedence instead.**


### CloudFormation-Lifecyclehooks 
---
- Lifecycle hooks enables you to perform custom actions by pausing the instance as an auto scaling group launches or terminates them
- When an instance is paused, it stays in the wait state until you complete the Lifecycle using CompleteLifeAction command or CompleteLifeAction operation or timeout period ends(default is one hour)

- EC2-Instance-Launching - install or configure software, before launching, in wait state
- EC2-Instance-Terminating - download logs or other data, before terminating, in wait state

### AWS-CodePipeline
---
-  includes a number of actions that help you configure build, test, and deploy resources for your automated release process.
-  can use the console, AWS CLI, or AWS CloudFormation to add cross-region actions in pipelines.
-  When AWS provider is the provider for an action and this actiontype/provider type are in different region from your pipelne, then called cross-region action.
-  If you use console to create pipeline, default artifact buckets are configured in the same region
-  If CloudFormation, CLI, SDK are used, provide artifact bucket for each region you have actions.
-  must create the artifact bucket and encryption key in the same AWS Region as the cross-region
 action and in the same account as your pipeline.
-  cannot create cross-region actions for the following action types: source actions, third-party actions, and custom actions. 

#### custom job worker

-  If your release process includes activities that are not included in the default actions, such as an internally developed build process or a test suite, you can create a custom action for that purpose and include it in your pipeline. 
-  When you create a custom action, you must also create a job worker that will poll CodePipeline for job requests for this custom action, execute the job, and return the status result to CodePipeline.
-  This job worker can be located on any computer or resource as long as it has access to the public endpoint for CodePipeline. 
-  To easily manage access and security, consider hosting your job worker on an Amazon EC2 instance.

![image](https://user-images.githubusercontent.com/81581601/157349915-ff94a6cf-5272-45e1-a993-ae87f764bb3f.png)

#### Monitoring

- Monitoring is an important part of maintaining the reliability, availability, and performance of AWS CodePipeline.
- Amazon CloudWatch Events — Use Amazon CloudWatch Events to detect and react to pipeline execution state changes (for example, send an Amazon SNS notification or invoke a Lambda function).
- AWS CloudTrail — Use CloudTrail to capture API calls made by or on behalf of CodePipeline in your AWS account and deliver the log files to an Amazon S3 bucket. You can choose to have CloudWatch publish Amazon SNS notifications when new log files are delivered so you can take quick action.
- Console and CLI — You can use the CodePipeline console and CLI to view details about the status of a pipeline or a particular pipeline execution.

### Lifecycle-Hook
---
- The EC2 instances in an Auto Scaling group have a path, or lifecycle, that differs from that of other EC2 instances.
- ![image](https://user-images.githubusercontent.com/81581601/156870225-90dc753b-1b27-4e13-9a2a-b256afdb9a24.png)
- CloudWatch agent is the most suitable tool to use to collect the logs.
- You can store and view the metrics in CloudWatch . The default namespace for metrics collected by the CloudWatch agent is CWAgent, although you can specify a     different namespace when you configure the agent.
 
### ECS
---
#### Deployment-AppSpec
- Hooks in Appspec depends on the compute platform for your deployment
- You can use a Lambda function to validate part of the deployment of an updated Amazon ECS application.
- Some lifecycle events are hooks that only execute Lambda functions specified in the AppSpec file.
- If rollbacks are configured, you can configure a CloudWatch alarm that triggers a rollback when the validation test in your Lambda function fails.x`

#### ECS-Agent

- Running service can be updated - number of tasks, task definition, change platfoem version fargate, scale up/dowm
- For updated docker image, create new task definition with that image and deploy in your service.
- If updated docker image uses same tag, keep current settings of your service and force new deployment.
- The new tasks launched by the deployment pull the current image/tag combination from your repository when they start.
- he service scheduler uses the minimum healthy percent and maximum percent parameters (in the deployment configuration for the service) to determine the deployment strategy.

### SSM
---
- Systems Manager Automation simplifies common maintenance and deployment tasks of Amazon EC2 instances and other AWS resources.
- Automation enables you to do the following.
    – Build Automation workflows to configure and manage instances and AWS resources.
    – Create custom workflows or use pre-defined workflows maintained by AWS.
    – Receive notifications about Automation tasks and workflows by using Amazon CloudWatch Events.
    – Monitor Automation progress and execution details by using the Amazon EC2 or the AWS Systems Manager console.
- Automation offers one-click automations for simplifying complex tasks such as creating golden Amazon Machines Images (AMIs), and recovering unreachable EC2 instances.
- Use the AWS-UpdateLinuxAmi and AWS-UpdateWindowsAmi documents to create golden AMIs from a source AMI. You can run custom scripts before and after updates are applied. You can also include or exclude specific packages from being installed.
-  – Use the AWSSupport-ExecuteEC2Rescue document to recover impaired instances.




---
## Table of contents
---
* [AWS-managed-policies](#awsmanaged-policies)
* [AutoScalingGroup-UpdatePolicy](#ASG-UpdatePolicy)
* [CloudFormation-Lifecycle hooks](#CloudFormation-Lifecyclehooks)
* [AWS-CodePipeline](#AWS-CodePipeline)


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
-  must create the artifact bucket and encryption key in the same AWS Region as the cross-region action and in the same account as your pipeline.
-  cannot create cross-region actions for the following action types: source actions, third-party actions, and custom actions. 



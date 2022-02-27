---
## Table of contents
---
* [AWS-managed-policies](#awsmanaged-policies)
* [AutoScalingGroup-UpdatePolicy](#ASG-UpdatePolicy)


### 'AWS-managed policies'
---

#### AWSCodeCommitFullAccess – Grants full access to CodeCommit. 
You should apply this policy only to administrative-level users to whom you want to grant full control over CodeCommit repositories
and related resources in your AWS account, including the ability to delete repositories.

#### AWSCodeCommitPowerUser – Allows users access to all of the functionality of CodeCommit and repository-related resources,
except it does not allow them to delete CodeCommit repositories or create or delete repository-related resources in other AWS services,
such as Amazon CloudWatch Events. It is recommended to apply this policy to most users.

#### AWSCodeCommitReadOnly – Grants read-only access to CodeCommit and repository-related resources in other AWS services,
as well as the ability to create and manage their own CodeCommit-related resources
(such as Git credentials and SSH keys for their IAM user to use when accessing repositories). 
You should apply this policy to users to whom you want to grant the ability to read the contents of a repository, but not make any changes to its contents.

Remember that  you can’t modify these AWS-managed policies . In order to customize the permissions, you can add a Deny rule to the IAM Role in order to block certain capabilities included in these policies.


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


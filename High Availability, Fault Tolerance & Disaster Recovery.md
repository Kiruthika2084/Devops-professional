---
## Table of contents
---
  * [EB-Deployment-policies](#EB-deployment-policies)
  * [Lambda<->API-gateway](#Lambda-APIgateway)
  * [Canary-deployment](#Canary-deployment)
  * [cross-region snapshot](#cross-region snapshot)


### EB-deployment-policies
---
- Elastic beanstalk deployment options are **All at once, Rolling, Rolling with additional batch, Immutable**.
- By default, uses all-at-once. If environment created via EB CLI, uses rolling deployment.

#### All at once
- Deploy the new version to all instances simultaneously. All instances in your environment are out of service for a short time while the deployment occurs. 

#### Rolling
- EB splits the environments EC2 instances into batches and deploys the new version one batch at a time. During rolling deployment some instances have old version and some serves the new version.

#### Rolling with additional batch
- maintains full capacity. A new batch of instances are launched and when the deployment completes, EB terminates the additional batch of instances.

#### Immutable
- launches a full set of new instances running new version in a seperate ASG, alongside old instances.
- 
----------------


### Lambda-APIgateway
---
- A Lambda Alias is like pointer to a specific version. Each Alias has unique ARN.
- Can update Alias to point to newer version of the function.
- Event sources use Lambda function Alias in the mapping configuration.
- In the resource policy, can grant permisions for event sources to use Lambda specifying the Alias ARN. No need to change later when version updates.
- Can point an alias to use maximum of 2 Lambda functions, distributing the traffic.

- In API gateway, create a canary deployment with canary settings in deployment creation operation.
- Create canary release deployment from non-canary release deployment by making a stage:update request.
- non-existing stage name can be used for non-canary release deployment, but not in canary-deployment(throws error)

### Canary-deployment
---
-To properly implement the canary deployment, you should do the following steps:

 *Use a router or load balancer that allows you to send a small percentage of users to the new version.
 *Use a dimension on your KPIs to indicate which version is reporting the metrics.
 *Use the metric to measure the success of the deployment; this indicates whether the deployment should continue or rollback.
 *Increase the load on the new version until either all users are on the new version or you have fully rolled back.
 
 ### cross-region snapshot
 ---
 - When you copy a snapshot to an AWS Region that is different from the source snapshot’s AWS Region, the first copy is a full snapshot copy, even if you copy an incremental snapshot. 
 - A full snapshot copy contains all of the data and metadata required to restore the DB instance.
 - After the first snapshot copy, you can copy incremental snapshots of the same DB instance to the same destination region within the same AWS account.
 - An incremental snapshot contains only the data that has changed after the most recent snapshot of the same DB instance.
 - Incremental snapshot copying is faster and results in lower storage costs than full snapshot copying. 
 - Incremental snapshot copying across AWS Regions is supported for both unencrypted and encrypted snapshots. 
 - For shared snapshots, copying incremental snapshots is not supported.
 - For shared snapshots, all of the copies are full snapshots, even within the same region.
 - Depending on the AWS Regions involved and the amount of data to be copied, a cross-region snapshot copy can take hours to complete. 
 - when you copy a source snapshot that is a snapshot copy, the copy isn’t incremental because the snapshot copy doesn’t include the required metadata for incremental copies.

 

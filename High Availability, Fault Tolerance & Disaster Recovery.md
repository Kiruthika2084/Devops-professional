---
## Table of contents
---
  * [EB-Deployment-policies](#EB-deployment-policies)
  * [Lambda<->API-gateway](#Lambda-APIgateway)


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

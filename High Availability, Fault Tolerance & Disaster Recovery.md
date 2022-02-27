---
## Table of contents
---
  * [EB-Deployment-policies](#EB-deployment-policies)


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

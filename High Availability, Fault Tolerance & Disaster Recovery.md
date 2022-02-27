---
## Table of contents
---
  * [EB-Deployment-policies](#EB-deployment-policies)


### EB-deployment-policies
---
AWS Elastic Beanstalk provides several options for how deployments are processed, including deployment policies (All at once, Rolling, Rolling with additional batch, and Immutable) and options that let you configure the batch size and health check behavior during deployments. **By default, your environment uses all-at-once deployments**. If you created the environment with the EB CLI and it’s an automatically scaling environment (you didn’t specify the --single option), it uses rolling deployments.

#### All at once
Deploy the new version to all instances simultaneously. All instances in your environment are out of service for a short time while the deployment occurs. 

#### Rolling
With rolling deployments, Elastic Beanstalk splits the environment’s EC2 instances into batches and deploys the new version of the application to one batch at a time, leaving the rest of the instances in the environment running the old version of the application. During a rolling deployment, some instances serve requests with the old version of the application, while instances in completed batches serve other requests with the new version.

#### Rolling with additional batch
To maintain full capacity during deployments, you can configure your environment to launch a new batch of instances before taking any instances out of service. This option is known as a rolling deployment with an additional batch. When the deployment completes, Elastic Beanstalk terminates the additional batch of instances.

#### Immutable
Immutable deployments perform an immutable update to launch a full set of new instances running the new version of the application in a separate Auto Scaling group, alongside the instances running the old version. Immutable deployments can prevent issues caused by partially completed rolling deployments. If the new instances don’t pass health checks, Elastic Beanstalk terminates them, leaving the original instances untouched.

----------------
If your application doesn’t pass all health checks, but still operates correctly at a lower health status, you can allow instances to pass health checks with a lower status, such as Warning, by modifying the Healthy threshold option. If your deployments fail because they don’t pass health checks and you need to force an update regardless of health status, specify the Ignore health check option.

When you specify a batch size for rolling updates, Elastic Beanstalk also uses that value for rolling application restarts. Use rolling restarts when you need to restart the proxy and application servers running on your environment’s instances without downtime.

AWS Elastic Beanstalk provides support for running Amazon Relational Database Service (Amazon RDS) instances in your Elastic Beanstalk environment. This works great for development and testing environments. However, it isn’t ideal for a production environment because it ties the lifecycle of the database instance to the lifecycle of your application’s environment.

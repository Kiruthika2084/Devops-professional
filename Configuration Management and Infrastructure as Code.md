---
## Table of contents
---
* [Cloud-watch metrics<->CodeDeploy deployment group](#cloudwatch-metrics-codedeploy)
* [AWS-systems Manager](#AWS-systems-manager)

#### cloudwatch-metrics<->CodeDeploy deployment group
---
- Create cloudwatch alarms for an instance or Amazon EC2 ASG in your codedeploy operations. 
- Alarm watches for metric and invoke actions when state changes.
- Can take actions like sending SNS, stopping, terminating or recovering an instance.
- Can configure to stop deployment when alarm is activated.
- **Can associate upto ten cloudwatch alarms with a codedeploy deployment group**
- If any of the alarms are activated, the deployment stops and the status is updated to stopped. 
  To use this option, grant Cloudwatch permissions to your codedeploy service role.

#### AWS Systems manager
---
- **Run command**- Remotely and securely manage the configuration of managed instances(machine in hybrid environment configured for systems manager)
- can use run command from console,cli, tool for powershell, sdk at no additional cost
- Administrators use run command for bootstrap,build deployment pipeline,configure log files, join instances to windows domain etc
- **parameter store** -store data such as passwords, licence codes, database strings as parameter values

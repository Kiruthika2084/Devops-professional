##AWS-managed policies that you can use for providing CodeCommit access.

AWSCodeCommitFullAccess – Grants full access to CodeCommit. 
You should apply this policy only to administrative-level users to whom you want to grant full control over CodeCommit repositories
and related resources in your AWS account, including the ability to delete repositories.

AWSCodeCommitPowerUser – Allows users access to all of the functionality of CodeCommit and repository-related resources,
except it does not allow them to delete CodeCommit repositories or create or delete repository-related resources in other AWS services,
such as Amazon CloudWatch Events. It is recommended to apply this policy to most users.

AWSCodeCommitReadOnly – Grants read-only access to CodeCommit and repository-related resources in other AWS services,
as well as the ability to create and manage their own CodeCommit-related resources
(such as Git credentials and SSH keys for their IAM user to use when accessing repositories). 
You should apply this policy to users to whom you want to grant the ability to read the contents of a repository, but not make any changes to its contents.

Remember that you can’t modify these AWS-managed policies. In order to customize the permissions, you can add a Deny rule to the IAM Role in order to block certain capabilities included in these policies.

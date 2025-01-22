# Setting Up IAM Policies 
## Objective
This project demonstrates the creation of an IAM user with restricted access and the assignment of custom policies to control which AWS services the user can access. It includes testing access to AWS services to verify that permissions are working as intended.

## Tasks Covered
- Creating an IAM user named restricted-user.
- Creating custom policies to grant full access to EC2 and S3. 
- Testing access to S3 and EC2 by logging in as restricted-user.
- Verifying that access to other AWS services (e.g., IAM) is denied due to policy restrictions.
____________________________________________________________________________________________________________________________________________________________
### User Details
![restricted user](https://github.com/user-attachments/assets/5b617124-46fe-4cf7-9182-6f75b988f258)
- In this step, I created an IAM user named "restricted-user".
- I gave the user access to the AWS Management Console by setting a custom password for login.
- While AWS recommends using Identity Center for managing users, I decided to create an IAM user to simplify permissions for this project.
_________________________________________________________________________________________________________
### Assigned Policies

#### S3 Access  
![s3 access only policy](https://github.com/user-attachments/assets/b8eff2ab-897d-4d41-bd07-939c0a5c7f9c)

This policy allows the user to retrieve files from all S3 buckets without restriction. However, it does not permit other actions like listing bucket contents or uploading files.

`"Version": "2012-10-17"`: This specifies the version of the policy language being used. "2012-10-17" is the most common and current version for AWS IAM policies.

`"Statement"`: A statement is the core of the policy. It defines the permissions.

`"Sid": "S3Accessonly"`: The Sid (Statement ID) is an optional identifier for the statement. Here, it's named "S3Accessonly" to clarify that this statement allows access to S3 resources.

`"Effect": "Allow"`: Specifies whether the action is allowed or denied. "Allow" grants permission, while "Deny" would explicitly block access.

`"Action": "s3:GetObject"`: Defines the specific S3 action the policy permits. `"s3:GetObject"` allows the user to retrieve objects from S3 buckets.

`"Resource": "*"`: Specifies the AWS resources the policy applies to. `"*"` grants access to all S3 buckets and objects.

#### EC2 Access
![start-stop instances policy](https://github.com/user-attachments/assets/56c32efe-1da0-4353-ac43-126925c48e4b)

This policy allows the user to start and stop EC2 instances across all resources. However, it does not permit other actions like launching new instances or terminating existing ones.

`"Version": "2012-10-17"`: This specifies the version of the policy language being used. "2012-10-17" is the most common and current version for AWS IAM policies.

`"Statement"`: A statement is the core of the policy. It defines the permissions.

`"Sid": "EC2Access"`: Optional identifier that clarifies the purpose of the statement, which in this case is granting specific EC2 access.

`"Effect": "Allow"`: Specifies whether the action is allowed or denied. "Allow" grants permission, while "Deny" would explicitly block access.

`"Action": ["ec2:StartInstances", "ec2:StopInstances"]`: These actions allow the user to start stopped instances, and stop running instances.

`"Resource": "*"`: Specifies the AWS resources the policy applies to. `"*"` grants access to all EC2 instances within the account.
____________________________________________________________________________________________________________________
After creating and assigning the custom policies to the restricted-user, I proceeded to test the policies by logging in as the user to ensure the permissions were applied correctly. This allowed me to verify that the user could access EC2 and S3 as expected, while being restricted from actions outside of the specified permissions, such as accessing IAM.
____________________________________________________________________________________________________________________________________________________________
### Testing the IAM User
#### Access to S3 Granted
![restricted user has access to s3](https://github.com/user-attachments/assets/510616ab-abe1-47ea-8a80-c00d06d688bf)

The screenshot shows the "Create a Bucket" page, confirming that the user has access to S3

#### Access to EC2 Granted
![restricted user has access to ec2](https://github.com/user-attachments/assets/3e0691f9-34d0-46c6-ae5a-5579ff045bd6)

The screenshot shows the "Create an EC2 Instance" page, confirming that the user can access EC2

#### Denied Access to IAM
![restricted user denied IAM access](https://github.com/user-attachments/assets/43e7d758-bae0-4016-a27f-cdee5eadc27e)
The screenshot shows an "Access Denied" message when attempting to access IAM, confirming that the restricted-user cannot manage IAM resources due to the lack of permissions for IAM actions in the assigned policies.

_________________________________________________________________________________________________________________________
## Lessons Learned

- IAM policies define the scope of actions users can perform. Each policy attached to an IAM user or group determines the specific resources they can access.

- Explicit permissions are required for each AWS service. Without a policy for a specific service, users are denied access by default.
  
- Testing permissions ensures that policies work as expected. Verifying access helps ensure that users have only the intended access and no more.
  
- IAM is a critical component for secure AWS management. Following the principle of least privilege helps reduce security risks.
  
- Error messages provide insight into denied access. These messages help identify missing permissions and refine policy settings.

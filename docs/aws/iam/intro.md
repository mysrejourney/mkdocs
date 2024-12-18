# IAM (Identity and Access Management)

IAM is a global service in AWS.
We can create users and these users can be grouped as well.
User can belong to the multiple groups, and the permission can be aggregated in this case.
At the same time, user cannot be part of any group either. 

`Group should have only users, not any other group.`

## Permission (Policy)

IAM permission is nothing but a policy document assigned to the user or group.
This is just a JSON document that describes what the user or group can do or cannot do.

`Remember that you have to follow least privileage to the user in AWS. Do not give more permissions to the user than what they really needed`


## Creating Group

1. Go to IAM service. Click on 'User Groups' menu.

![aws_165.png](../../assets/aws_165.png)

2. Click on 'Create Group' button

![aws_166.png](../../assets/aws_166.png)

3. Enter the group name and select the predefined policy based on your requirement. Here I am selecting administrator 
policy that has full access.

![aws_167.png](../../assets/aws_167.png)

4. Click on 'Create Group' button

![aws_168.png](../../assets/aws_168.png)

## Creating User

1. Go to IAM service. Click on 'Users' menu.

![aws_169.png](../../assets/aws_169.png)

2. Click on 'Create User' button

![aws_170.png](../../assets/aws_170.png)

3. Enter the username and click on 'Next' menu.

![aws_171.png](../../assets/aws_171.png)

4. Here we are creating the new user and mapping the user with 'admin' group. It means that the new user has all 
the permissions provided to the group 'admin'

Select the permission option and choose the group. Click on 'Next' button.

![aws_172.png](../../assets/aws_172.png)

5. Click on 'Add tag' button

![aws_173.png](../../assets/aws_173.png)

6. Click on 'Create user' button

![aws_174.png](../../assets/aws_174.png)

Now the user is created and this user is part of 'admin' group.

![aws_175.png](../../assets/aws_175.png)

7. Create the password for newly created user. Click on the username and then click on 'Security Credential' tab.
Click on an 'Enable console access' button.

![aws_176.png](../../assets/aws_176.png)

8. Select a custom password option and then enter the password. Click on an 'Enable console access' button.

![aws_177.png](../../assets/aws_177.png)


`Now, the user is created and have a console access. This user can login using his/her IAM username and password`

## IAM Policy Inheritance


Assume that there are three different groups (Developers, Audit, Operations)
and six team members (Alice, Bob, Charles, David, Edward and Fred) are part of those groups. 

![aws_178.png](../../assets/aws_178.png)

Each group has different policy and hence they have different access to the services.
User `Fred`  is not part of any group, and he has his own permission.
Users 'Charles and David' belong to two different groups, and they have both group policy access as well.

## IAM Policy Structure

Policy defines what action user can perform on the services.

| **Name**  | **Description**                                  |
|-----------|--------------------------------------------------|
| Version   | Always "2012-10-17"                              |
| Statement | One or more statements required                  |
| Sid       | Can be anything (optional)                       |
| Effect    | Either "Allow" or "Deny"                         |
| Principal | User/Group/Account to the policy applied to      |
| Action    | List of actions can be performed on the services |
| Resource  | What kind of actions applied to the resources    |
| Condition | Condition when the policy is effect              |


![aws_179.png](../../assets/aws_179.png)


## Creating Policy

I am creating the new user, and this user is not part of any group. We can define the policy what this new user can do.

![aws_180.png](../../assets/aws_180.png)

As of now, the user 'pandian' is created and there is no policy attached to this user.

![aws_181.png](../../assets/aws_181.png)

Now I am trying to view the users created so far using the newly created user 'pandian'
It clearly shows that this new user 'pandian' doesn't have permission to view the user list (Access denied).

![aws_182.png](../../assets/aws_182.png)

Now, let us give the permission to get and list the users for 'pandian'.
To do this, you need to log in with admin-privileged user.
Click on the username 'pandian' and click on 'Add permission' dropdown menu.

![aws_183.png](../../assets/aws_183.png)

Click on 'Add permission' button

![aws_184.png](../../assets/aws_184.png)

Choose 'Attach policies directly' option. Search 'IAMReadOnlyAccess' policy.

![aws_185.png](../../assets/aws_185.png)

Click on 'Next' button. Review the details and Click on 'Add permission' button.

![aws_186.png](../../assets/aws_186.png)

Now the newly created user 'pandian' has one policy attached to it.

![aws_187.png](../../assets/aws_187.png)

User 'pandian' is able to view the user list now. But he cannot create any group or user.

![aws_188.png](../../assets/aws_188.png)

![aws_189.png](../../assets/aws_189.png)


## Create inline policy

Let us give the permission to get and list the users for 'pandian'.
To do this, you need to log in with admin-privileged user.
Click on the username 'pandian' and click on 'Add permission' dropdown menu.

![aws_183.png](../../assets/aws_183.png)

Click on 'Create inline policy' button

![aws_190.png](../../assets/aws_190.png)

Select the services from the dropdown.
Choose the access level (List/Read/Write/Permission Management/Tagging) for the service.

![aws_191.png](../../assets/aws_191.png)

Enter the policy name, and click on 'create policy' button.

![aws_192.png](../../assets/aws_192.png)


## Create User, Group, Policy in AWS CLI

**Prerequisite**

1. AWS cli should be installed.
2. AWS access key should be created.
2. AWS configure should be done. 


### Create Access Key

1. Create the access key for IAM user.

Let us create an access key for the user 'satheesh'.

![aws_193.png](../../assets/aws_193.png)

2. Click on the 'create access' button.
3. Select 'CLI' option and click on 'Next' button.

![aws_194.png](../../assets/aws_194.png)

4. Click on 'create access key' button

![aws_195.png](../../assets/aws_195.png)

5. Note down the access key and secret key. This will be used for configuration.

### AWS Configuration Steps

1. AWS CLI installed already on my machine. Refer "https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" for the steps.

![aws_196.png](../../assets/aws_196.png)

2. Execute `aws configure` command. Provide the required details like access key, secret key, region and output format.

![aws_197.png](../../assets/aws_197.png)

Now, it is configured. We can run any aws command from the terminal.

### Create User

1. Run the command

```html

aws iam create-user --user-name <UserName>

```

```html
aws iam create-user --user-name praba

```
![aws_198.png](../../assets/aws-198.png)

![aws_199.png](../../assets/aws_199.png)
    

2. Attach the IAM policy to the user

```html
aws iam attach-user-policy --user-name <UserName> --policy-arn arn:aws:iam::aws:policy/<Policy name>
```

```html
aws iam attach-user-policy --user-name praba --policy-arn arn:aws:iam::aws:policy/IAMReadOnlyAccess
```

![aws_200.png](../../assets/aws_200.png)

3. Verify the user

```html
aws iam list-users
```

![aws_201.png](../../assets/aws_201.png)

### Create Group

1. Run the command

```html

aws iam create-group --group-name <GroupName>

```

```html
aws iam create-group --group-name sre-team-members

```
![aws_202.png](../../assets/aws_202.png)

![aws_203.png](../../assets/aws_203.png)
    

2. Attach the IAM policy to the group

```html
aws iam attach-group-policy --group-name <GroupName> --policy-arn arn:aws:iam::aws:policy/<Policy name>
```

```html
aws iam attach-group-policy --group-name sre-team-members --policy-arn arn:aws:iam::aws:policy/IAMFullAccess

```

![aws_204.png](../../assets/aws_204.png)


3. Add the user to the group

```html
aws iam add-user-to-group --group-name <GroupName> --user-name <UserName>
```

```html
aws iam add-user-to-group --group-name sre-team-members --user-name praba
```

![aws_205.png](../../assets/aws_205.png)

4. Verify the group

```html
aws iam list-groups
```

![aws_206.png](../../assets/aws_206.png)

### Create Policy

1. Define the policy in the JSON format.  Below policy gives full access to IAM service

`policy.json`

```html
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:*",
      "Resource": "*"
    }
  ]
}
```

![aws_207.png](../../assets/aws_207.png)

2. Create policy

```html
aws iam create-policy --policy-name my-iam-full-access-policy --policy-document file://policy.json

```

![aws_208.png](../../assets/aws_208.png)

3. Verify the policy

```html
aws iam list-policies
```

![aws_209.png](../../assets/aws_209.png)


## IAM Roles

If some of the AWS services want to perform some action on our behalf,
then we need to assign permission to those services.
This permission is called as 'Roles'.

![aws_210.png](../../assets/aws_210.png)

### Create Role

1. Go to IAM service. Click on the 'Roles' menu.

![aws_211.png](../../assets/aws_211.png)

2. Select the service and click on 'Next' button

![aws_212.png](../../assets/aws_212.png)

3. Select the policy and click on 'Next' menu.

![aws_213.png](../../assets/aws_213.png)

4. Enter the role name and click on 'Create role' button.

![aws_214.png](../../assets/aws_214.png)

Now the role is created.

### Create Role using AWS CLI

1. Define policy

`policy.json`

```html
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

2. Create the role

```html
aws iam create-role --role-name <RoleName> --assume-role-policy-document file://trust-policy.json
```

```html
aws iam create-role --role-name my-ec2-role --assume-role-policy-document file://policy.json
```

![aws_215.png](../../assets/aws_215.png)

3. Attach a Policy to the Role

```html
aws iam attach-role-policy --role-name <RoleName> --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

```html
aws iam attach-role-policy --role-name my-ec2-role --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

![aws_216.png](../../assets/aws_216.png)

4. Verify the Role

```html
aws iam get-role --role-name <RoleName>
```

```html
aws iam get-role --role-name my-ec2-role
```

![aws_217.png](../../assets/aws_217.png)


## IAM Security Tools

1. IAM Credential Report (Account level) - Report the list of users and their current status in account level.
2. IAM Access Advisor (User level) - Shows the service permission for each user and when the user last accessed the service.


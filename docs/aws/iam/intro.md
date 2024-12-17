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




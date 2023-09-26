#Terraform State
When you run `terraform apply` command, the state file is created. If this command is NOT executed once, then the state file WILL NOT create at all.
When we are running the command `terraform apply`, terraform refresh the state in memory and see if there is any resource created with same configuration.
If it was already created, then the resources will not be created. Else, it will create with new `id`.
<mark>The state file is JSON data structure, and it has complete information about the infrastructure created by terraform.</mark>

This state file will be used by `terraform plan` and `terraform apply` commands to compare the existing infrastructure information
and take the necessary action accordingly.
When terraform creates the resource, it records all the information in the state. <mark>All resources created by terraform
would have a unique id which is used to identify the resource in the real world.</mark> Also, state file tracks the resource dependency as well.

If any resource is depending upon another resource, then it will NOT create until dependant resource created. This will improve performance
as it refers local state file and skip if the resources are already available (Terraform store caches of attribute values). 
<mark>We can inform terraform that it can only refer the local state file using the below command</mark>
```
terraform plan --refresh = false

OR

terraform apply --refresh = false
```

Note that <mark>state file contains all the information including sensitive information. Hence, you need to make sure that it will not be kept
for public or source control system (GitHub/bitbucket).</mark> Instead, it can be stored at AWS S3, Google cloud storage etc., 
Remember that we should NOT edit the state file. If we need to edit (if it is mandatory), we need to use terraform command.
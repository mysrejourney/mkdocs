#Work with Terraform

**Lifecycle Rules**

By default, Terraform first destroy the resources first and then will create a new resource.

**Example**

You have local file creating configuration file your directory and the resource was provided already.
Now, you want to make a changes in the content of the file like below
```main.tf
resource "local_file" "my-file" {
    filename="./test.txt"
    content="Satheesh Pandian" // earlier it is "Satheesh"
}
```

When you run `terraform apply` command. it destroys the existing file first, and then it will create new one.

![terraform_default.png](../assets/terraform_default.png)

***Create first and Destroy then***

If you want to change this behaviour, you can use lifecycle rules.

```main.tf
resource "local_file" "my-file" {
    filename="./test.txt"
    content="My SRE Journey" // earlier it is "Satheesh Pandian Jeganthan"
    
    lifecycle {
        create_before_destroy = true
    }
}
```

![terraform_create_destroy.png](../assets/terraform_create_destroy.png)

***Do not destroy***

If you DO NOT want to destroy any resource, then you need to use the below lifecycle rules.
This will be used when you deal with database. Most of the time, we DO NOT want to delete database while changing something. 
So, you need to update lifecycle rule with `prevent_destroy = true`.

```main.tf
resource "local_file" "my-file" {
    filename="./test.txt"
    content="My SRE Journey" // earlier it is "Satheesh Pandian Jeganthan"
    
    lifecycle {
        prevent_destroy = true
    }
}
```

![terraform_prevent_destroys.png](../assets/terraform_prevent_destroys.png)


`terraform destroy` command still destroys the resource even if you mentioned lifecycle rule with `prevent_destroy = true` 
in the configuration file.

***Ignore changes***

If you DO NOT want to create any resource in case of any particular attribute change. In the below
example, I am making changes in `content`

```main.tf
resource "local_file" "my-file" {
    filename="./test.txt"
    content="Satheesh Pandian Jeganthan" // earlier it is "I am SRE in Bangalore"
    
    lifecycle {
        ignore_changes = [content] // you can any number of attribute in the list
    }
}
```

![terraform_ignore_changes.png](../assets/terraform_ignore_changes.png)


`ignore_changes = all` <mark>means that it won't create any resource even if there is any change in any attribute.</mark>

**QUICK SUMMARY**

![terraform_lifecycle_rules.png](../assets/terraform_lifecycle_rules.png)

<mark>It is better NOT to use `create_before_destroy = true` lifecycle rule for local file 
because the rule will create the local file first and the same file to be destroyed during the recreate operation.</mark>

**Data Sources**

If you want to read the data from any file which are in your current configuration directory, but not created/maintained by terraform.
In that case, you can use that file as a data resource.

```
>cat data.txt
I am Satheesh from Bangalore and I am working as Sr.SRE in a bank.
```

The above file is created manually without using terraform commands. Also, terraform does not have any information 
about this file so far.

```html
resource "local_file" "my-file" {
    filename = "./test.txt"
    content = data.local_file.my-data.content
    lifecycle {
        create_before_destroy = true
    }
}
    
data "local_file" "my-data" {
    filename="./data.txt"
}
```

![terraform_datasources.png](../assets/terraform_datasources.png)

`Remember, you CAN NOT do create/update/destroy for data sources. You can ONLY do read the data source`

**Meta Argument - Count**

```html
resource "local_file" "my-file" {
    filename = "./test.txt"
    content = "Satheesh"
    count = 3
}
```

![terraform_count_basic.png](../assets/terraform_count_basic.png)

However, the problem is here that there is ONLY one file created instead of 3. This is because the filename 
is not unique. Hence, terraform is recreated the same file again and again.

![terraform_count_ls.png](../assets/terraform_count_ls.png)

Hence, we need to create three different file. Here, I used variable configuration file for creating three files and modified
configuration file to read the filename from variable configuration.
```
variable filename {
    default = ["./test.txt","./sample.txt","./exam.txt"]
}
```

```
resource "local_file" "my-file" {
    filename = var.filename
    content = "Satheesh"
    count = 3
```

![terraform_count_number_3.png](../assets/terraform_count_number_3.png)

![terraform_count_number_3_output.png](../assets/terraform_count_number_3_output.png)

In the above example, even if you have 100 arguments in variable configuration file, this will ALWAYS create 3 files as 
we hardcoded `count = 3`. To create the number of files defined in variable configuration file, we need to update the main
configuration file to pick the length of the list variable.

```
resource "local_file" "my-file" {
    filename = var.filename
    content = "Satheesh"
    count = length(var.filename)
```

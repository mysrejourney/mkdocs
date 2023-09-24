#Terraform

Terraform is a IAC tool, specifically <mark>used for provisioning</mark>. 
It is an open source tool <mark>developed by Hashicorp</mark>.
It is allowing us to build image, manage and destroy infrastructure in few minutes. 
The biggest advantages of terraform is that it can <mark>support multiple platforms</mark> including private and public cloud providers such as Azure/AWZ/GCP/VMware/Physical machines.

Providers (AWS/Azure/GCP etc.,) helps terraform to manage the third party platforms through their APIs. 
Terraform uses HCL(Hashicorp Configuration Language) which is very simple language to define the infrastructure <mark>resources to be provisioned as a block of code.</mark>
All infrastructure resources are defined in configuration files with `tf` extension.
The source code can be maintained in source control system. So, it can be distributed to other teams as well.

`NOTE: Remember, every objects that terraform manages known as resources. 
Terraform manages the object's entire life cycle starting from provisioning to destroying`

Terraform has <mark>three phases</mark>
<ul>
    <li>Init</li>
    <li>Plan</li>
    <li>Apply</li>
</ul>

In `init` phase, <mark>terraform initiates the project and identify the providers.</mark>
This provider will be used in the targeted environment.

In `plan` phase, <mark>terraform creates the plan to get the resources to target state.</mark>

In `apply` phase, <mark>terraform makes necessary changes to the plan to get the resources to desired state in the target environment.</mark>


Terraform maintains the record that state of the infrastructure.
Based on this record, it can decide what action can be taken when updating the resources in particular platform such as AWS and Azure.

It is Terraform's responsibility to maintain the defined state for all the resources in the code at all time.

Terraform can read the attribute of the existing resources by configuring datasource. This can be used to configure other datasource within Terraform.
It can also import other resources outside of Terraform and manages them.

##<span style="color:red">H</span>ashiCorp <span style="color:red">C</span>onfiguration <span style="color:red">L</span>anguage (HCL)



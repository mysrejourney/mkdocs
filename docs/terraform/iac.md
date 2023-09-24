#<span style="color:red">I</span>nfrastructure <span style="color:red">A</span>s <span style="color:red">C</span>ode (IAC)
In modern world technologies, provisioning infrastructure is the biggest challenge. There are lots of cloud providers who can help to provide resources such as virtual machines, networking, databases and storage devices etc., You can use any one of them and build/create your infrastructure based on your business need.

There are two ways you can obtain their resource provisioning.
<ol>
<li> Management Console</li>
<li> Through coding</li>
</ol>

Out of these two, the better way is to code the entire provisioning process. The reason for this is that you can write the code to define provision, configure, update and destroy all resources whenever you don't need them, and you can redo this process anytime without manual intervention. Whereas, in the management console, you need to do them manually every single time which is not the correct way.
This is called <mark>Infrastructure As Code (IAC)</mark>.

With IAC, we can define infrastructure resources using simple, human-readable  high level language. 

**Types of IAC tools**

<ol>
<li> Configuration Management</li>
    <ul>
        <li>Ansible</li>
        <li>Puppet</li>
        <li>Saltstack</li>
        <li>Chef</li>
    </ul>
<li> Server Templating</li>
    <ul>
        <li>Docker</li>
        <li>Vagrant</li>
        <li>Packer</li>
    </ul>
<li> Provisioning Tools</li>
    <ul>
        <li>Terraform</li>
        <li>Cloud Formation</li>
    </ul>
</ol>

***1.Configuration Management***

1. These are <mark>used to install and manage the software</mark> on existing infrastructure resources. 
2. It maintains the standard structure of the code (Not like we write the code for our need) and it can be reused. 
3. It designed to <mark>run in multiple resources at once</mark> (You can create and execute resources in multiple machine using single command).
4. Version control options (You can update/upload your ansible playbook/role into version control repo [ansible galaxy]).
5. They are <mark>idempotent.</mark> It means if the resources are already exist, we don't need to create them again. Those creating code can be skipped easily (For this, we don't need to write any logic, it can be handled by default) and move to next steps/process.

***2.Server Templating***

1. It is used to <mark>create a custom images of VMs/containers.</mark> These VMs/containers are already preinstalled all required software and dependencies.
2. <mark>Immutable infrastructure </mark>
   1. Once you deployed a VM/container, you CANNOT change their config. It remains unchanged. (This can be possible in configuration management tools such as Ansible)
   2. If you need to change, you can update the image and redeploy.


***3.Provisioning Tools***

1. These tools are <mark>used to provisioning the infrastructure components (can be servers/DBs/NW devices/storages/security groups/VPCs/services) using simple code.</mark>

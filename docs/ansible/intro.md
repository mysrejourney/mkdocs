# Introduction 

Ansible provides open-source automation that reduces complexity and runs everywhere. Here are some use cases 

1. Eliminate repetition
2. Manage and maintain system configuration

<mark>Ansible uses playbook to automate the tasks.</mark> You declare the desire state of your system in the playbook 
and ansible ensures that the system remains in the system.

### Advantages
1. Agentless - No need to install any agent to automate the system
2. Scalable - Easily scalable in any environment including cloud infrastructures.


### Ansible Concepts

- Control Node
    - This is the machine where you run Ansible commands in CLI tools. 
    - You can use any computer that meets the software requirements. 
    - <mark>You can run ansible as a container. Ansible uses the image in the container is called as execution environment.</mark>
    - An execution environment image contains the following packages as standard:
      - `ansible-core`, `ansible-runner`, `python` and ansible content dependencies

- Managed Node
    - These are the target device which you want to manage.
    - <mark>We don't need to install in these machines.</mark>

- Plays (Basic unit of Ansible execution)
    - This is nothing but an ordered list of tasks can be run repeatedly.
    - Play contains variables, roles, tasks and defines how to iterate over them.

- Playbooks
    - Playbook contains play. It is written in YAML. 
    - `ansible-playbook` command operates on this file.

- Roles
    - A reusable ansible content (tasks, variables, plugins etc.,) can be used in the play. 
    - To use any roles, it must be imported into the play.

- Tasks
    - Action to be applied to the managed nodes.

- Handlers
    - <mark>This is the task, but executed only when notified by the previous task which results in a changed status.</mark>

- Modules
    - The code copies to each managed nodes and executes to accomplish the task by Ansible.

- Plugins
    - Piece of code that expand Ansible's core capabilities. It can control how to you connect managed nodes, filter the data etc.,

- Collections
    - It is a format of ansible content such as roles, plugins, playbooks etc., 
    - You can install collections using Ansible Galaxy.
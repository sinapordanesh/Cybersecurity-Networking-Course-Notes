# 2_Introduction and Installing Ansible

# What is Ansible?

## What is Ansible?

- Ansible is an open-source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes.
- Ansible is both an automation language and an automation engine running Playbooks
- "Infrastructure as code". The idea is that server and client infrastructure maintenance should be treated the same as software development with proven, and executable solutions capable of running an organization regardless of changes.

![Screenshot 2023-06-19 at 2.56.04 PM.png](2_Introduction%20and%20Installing%20Ansible%20e9a5d42ceea542028ca3fa6b30e540ed/Screenshot_2023-06-19_at_2.56.04_PM.png)

## Ansible Architecture

- In Ansible, there are two categories of computers: the control node and managed nodes.
- Ansible works by connecting to nodes on a network, and then sending a small program called an Ansible module to that node.
- Managed hosts are listed in an inventory, which also organizes those systems into groups for easier management.
- Ansible executes these modules over SSH and removes them when finished.
- Your Ansible control node needs login access to the managed nodes.
- An Ansible module is written to be a model of the desired state of a system.

# Installing Ansible

- The Ansible software only needs to be installed on the control node.
- Managed hosts do not need to have Ansible installed as Ansible communicates over
SSH.
- You need a valid RedHat Automation Platform subscription on the control node. a Managed hosts running Linux need to have Python 3.6(or later) or Python 2.7 (or later)
installed.
- A user with administrative privileges should be created on the managed hosts to be used by Ansible.
- Managed Windows hosts need installed PowerShell 3.0 and .NET Framework 4.0(or later).

![Screenshot 2023-06-19 at 2.58.13 PM.png](2_Introduction%20and%20Installing%20Ansible%20e9a5d42ceea542028ca3fa6b30e540ed/Screenshot_2023-06-19_at_2.58.13_PM.png)

1. Make sure that your master and slave servers are running a valid Linux distribution, with Python 3.6+ or Python 2.7+ installed.
2. Install Ansible on the master server by running the following command:
    
    ```
    $ sudo yum install ansible
    ```
    
    This command installs Ansible and all its dependencies.
    
3. Configure SSH access from the master to the slave servers. Generate a public/private key pair on the master server using the following command:
    
    ```
    $ ssh-keygen
    ```
    
    Copy the public key to the slave servers using the following command:
    
    ```
    $ ssh-copy-id <username>@<slave_server_ip>
    ```
    
    Replace `<username>` with the username of the user on the slave server that you wish to use for Ansible, and `<slave_server_ip>` with the IP address of the slave server.
    
4. Verify that SSH access is working by running the following command on the master server:
    
    ```
    $ ssh <username>@<slave_server_ip>
    ```
    
    Replace `<username>` and `<slave_server_ip>` with the appropriate values.
    
5. Create an Ansible inventory file on the master server. This file should contain a list of all the slave servers that you wish to manage with Ansible. The inventory file should be located at `/etc/ansible/hosts`.
6. Test that Ansible is working by running the following command on the master server:
    
    ```
    $ ansible all -m ping -i inventory
    ```
    
    This command should return a success message for each of the slave servers listed in the inventory file.
    
7. You can now start creating Ansible playbooks to automate tasks on your slave servers.
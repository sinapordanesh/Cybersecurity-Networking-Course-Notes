# 3_Ansible Playbooks and Ad-hoc Commands

# Ansible Inventory

## What are Ansible Inventories?

- The Ansible inventory file defines on which hosts and/or groups of hosts commands, modules, and tasks in a playbook or ad-hoc command are operated on.
- The inventory file can list individual hosts or user-defined aroups of hosts. This enables you to define groups of devices on which to run certain commands.
- The default location for the inventory file is `/etc/ansible/hosts`.
- You can create project-specific inventory files in alternate locations.
- You can create project-specific inventory files in alternate locations which can be specified either in the configuration file, playbook or using the "¡" option for ad-hoc commands.
- An inventory can be written in INI or YAML format.

## Sample Inventory File

![Screenshot 2023-06-20 at 3.01.09 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-20_at_3.01.09_PM.png)

The picture above is a sample Ansible inventory file written in INI format. It lists three groups of hosts - "webservers", "dbservers", and "local". Each group is defined with a name enclosed in square brackets, followed by a list of hostnames or IP addresses. The "webservers" group has two hosts, "[www1.example.com](http://www1.example.com/)" and "[www2.example.com](http://www2.example.com/)". The "dbservers" group has one host, "[db.example.com](http://db.example.com/)". The "local" group has one host, "localhost". This file can be used to define where Ansible commands and playbooks are to be executed.

# Ansible Configuration File

- The way Ansible behaves is specified in the Ansible configuration file.
- By default, Ansible has a configuration file located at `/etc/ansible/ansible.cfg` which is used unless another configuration file takes precedence.
- If an `ansible.cfg` exists within the home directory of the user running it will take
precedence over the default `ansible.cfg` file.
- If an `ansible.cfg` file exists in the working directory in which the ansible command is
run, then that `ansible.cfg` file will take precedence over the last two stated.
- If the "ANSIBLE CONFIG" variable is defined then take will take precedence over the
last 3 stated.
- Settings are not cumulated from multiple files so anthing not stated within the
ansible configuration file will be set to the default value.

## Sample Config File

![Screenshot 2023-06-20 at 3.10.29 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-20_at_3.10.29_PM.png)

The picture above is a sample Ansible configuration file written in INI format. It defines various settings that control Ansible's behavior, such as the default inventory file location, the location of log files, and whether to use SSH control persistently. The comments provide additional information about each setting.

# Ansible Ad-hoc Commands

![Screenshot 2023-06-20 at 3.18.51 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-20_at_3.18.51_PM.png)

## Sample Ad-hoc Commands

![Screenshot 2023-06-20 at 3.19.10 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-20_at_3.19.10_PM.png)

![Screenshot 2023-06-20 at 3.21.23 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-20_at_3.21.23_PM.png)

## Basic Modules To Know

- Ping
    - It pings and you can check host accessibility
- User
    - Manages users on the managed host.
- Service
    - Manages services on the managed host.
- Copy
    - Copy a file to the managed host but can also be used to create content.
- Yum
    - Manage packages on the managed host.
- File
    - Manage files on the managed host.
- Firewalld
    - Manage the firewalld service on managed hosts
- Reboot
    - a Reboot the managed hosts.
- URI
    - • Interact with web content.
- Nmcli
    - Manage networking on the managed hosts.

## Some command examples

Here are some examples of Ansible ad-hoc commands:

- `ansible all -m ping`: Tests connectivity to all hosts in the inventory
- `ansible webservers -m command -a "uptime"`: Runs the `uptime` command on all hosts in the `webservers` group
- `ansible dbservers -m copy -a "src=/etc/motd dest=/etc/motd"`: Copies the file `/etc/motd` from the control node to the `/etc/motd` file on the `dbservers` group
- `ansible localhost -m file -a "path=/tmp/testfile state=touch"`: Creates an empty file `/tmp/testfile` on the control node
- `ansible all -a "df -h"`: Runs the `df -h` command on all hosts in the inventory
- `ansible all -m yum -a "name=nginx state=present"`: Installs the `nginx` package on all hosts in the inventory
- `ansible all -m reboot`: Reboots all hosts in the inventory

# Ansible Playbooks

![Screenshot 2023-06-21 at 2.43.43 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-21_at_2.43.43_PM.png)

- Playbooks are written in YAML format and saved usually with yaml or yml extension.
- They use spacing for indentation (children more than parents) so keep spacing constant!!
- Empty lines do not impact the playbook.
- The start of the playbook is "
- " (3 lines)
- Comments can be added using the "# character.
- Strings do not have to be in quotation, but it is recommended to use quotation for readability.
- You can write multiple plays within a playbook
- Tasks are executed in order from top to bottom.
- If a tasks fails then the playbook will stop, and no subsequent task will be run by default.

## Output Color Coding

![Screenshot 2023-06-21 at 2.44.49 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-21_at_2.44.49_PM.png)

## Sample

![Screenshot 2023-06-21 at 2.45.47 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-21_at_2.45.47_PM.png)

![Screenshot 2023-06-21 at 2.46.24 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-21_at_2.46.24_PM.png)

![Screenshot 2023-06-21 at 2.47.39 PM.png](3_Ansible%20Playbooks%20and%20Ad-hoc%20Commands%2020f63338cfc64fe398496c0cc59d2e23/Screenshot_2023-06-21_at_2.47.39_PM.png)

## Demo

1. **IF you are using VIM for file editing only**: in the main home directory of automation user in root server, create a file `.vimrc` and write the following on it:
    
    ```bash
    autocmd FileTypre yaml setlocal ai ts=2 sw=2 et
    ```
    
2. Make a directory at which is called playbooks: 
    
    `mkdir playbooks`
    
3. in the playbooks directory create files:
    1. `inventory`
    
    ```bash
    servera
    serverb
    [servers]
    servera
    serverb
    ```
    
    1. `ansible.cfg`
    
    ```bash
    [defaults]
    remote user=automation
    inventory=/home/automation/playbooks/inventory 
    [privilege escalation]
    become=true 
    become_method=sudo 
    become_user=root 
    become_ask_pass=false
    ```
    
    1. `playbook.yml`
    
    ```yaml
    ---
    - name: create user
    	become: true
      become_user: root 
    	hosts: all 
    	tasks:
    		- name: ensure user is created 
    			user:
    				name: test 
    				state: present
    ```
    
4. then, run:
    
    ```yaml
    ansible-playbook --syntax-check playbook.yml
    ```
    
5. Finally, run the command for automation:
    
    ```yaml
    ansible-playbook playbook.yml
    ```
    

## Different `state` values

- `present`: Ensures that a resource, such as a file or user, exists on the managed hosts. If the resource already exists, it will not be modified. If it doesn't exist, it will be created.
- `absent`: Ensures that a resource does not exist on the managed hosts. If the resource exists, it will be removed.
- `started`: Ensures that a service is started on the managed hosts. If the service is already running, nothing will happen. If it is stopped, it will be started.
- `stopped`: Ensures that a service is stopped on the managed hosts. If the service is already stopped, nothing will happen. If it is running, it will be stopped.
- `reloaded`: Ensures that a service is reloaded on the managed hosts. This is similar to `started`, but is used when a service has been updated and needs to be reloaded rather than restarted.
- `restarted`: Ensures that a service is restarted on the managed hosts. This will stop the service if it is running and start it again.
- `enabled`: Ensures that a service is enabled on the managed hosts. This means that the service will be started automatically when the system boots.
- `disabled`: Ensures that a service is disabled on the managed hosts. This means that the service will not be started automatically when the system boots.
- `latest` : Ensures Ansible will install the latest version of the package available from the configured repository.

## Playbook Samples

1. 

```yaml
---
- name: create user
	become: true
  become_user: root 
	hosts: all 
	tasks:
		- name: install apache2 
			apt:
				name: apache2 
				state: latest
		- name: start apache2
			service:
				name: apache2
				state: started 
```

This Ansible playbook installs the latest version of Apache2 and starts Apache2 as a service on all hosts. It performs privileged actions as the root user and executes on all hosts listed in the inventory file. The tasks section installs the Apache2 package using the `apt` module and starts the Apache2 service using the `service` module.

1. 

```yaml
---
- name: myplay 
	become: true 
	remote_user: automation 
	become_method: sudo 
	become_user: root 
	hosts: serverb 
	tasks:
		- name: create user test 
			user:
				name: test 
				state: present

- name: my second play 
	become: true 
	remote_user: automation 
	become_method: sudo 
	become_user: root 
	hosts: servers 
	tasks:
		- name: create a second user on both servers 
			user:
				name: test2 
				state: present
		- name: delete user test 
			user:
				name: test 
				state: absent
```

This YAML document has two plays, each of which has a name, some settings, and a list of tasks. Each task has a name and a module to run, with additional parameters as necessary.

The first play creates a user named "test" on the host "serverb". The second play creates a user named "test2" on all hosts in the "servers" group, and then deletes the user "test" from all hosts in the "servers" group.

The "become" settings enable privilege escalation, allowing certain tasks to be executed as the root user. "remote_user" specifies the user to connect as on the remote host. "hosts" specifies the hosts or groups of hosts that this play applies to.
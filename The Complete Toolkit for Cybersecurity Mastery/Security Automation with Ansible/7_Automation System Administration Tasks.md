# 7_Automation System Administration Tasks

# Manage `Users` and Groups Using Ansible

![Screenshot 2023-06-27 at 2.07.55 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.07.55_PM.png)

![Screenshot 2023-06-27 at 2.09.14 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.09.14_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    ---
    - name: creat users
    	hosts: all
    	become: true
    	tasks: 
    		- name: user module
    			user: 
    				name: sysadmin
    				state: present
    				groups: sina
    				append: yes
    				shell: /bin/bash
    				uid: 1049
    				comment: my comment
    				create_home: no
    ```
    
2. `playbook.yml`
    
    ```yaml
    ---
    - name: creat users
    	hosts: all
    	become: true
    	tasks: 
    		- name: user module
    			user: 
    				name: sysadmin
    				state: present
    				groups: sina
    				append: yes
    				shell: /sbin/nologin
    				uid: 1050
    				comment: my comment
    				create_home: yes
    				generate_ssh_key: yes
    				ssh_key_file: /home/sysuser/my_id
    ```
    
3. `playbook.yml`
    
    ```yaml
    ---
    - name: creat groups
    	hosts: all
    	become: true
    	tasks: 
    		- name: groupmodule
    			group: 
    				name: mynewgroup
    				state: present
    				uid: 10030
    				system: no
    ```
    

# Manage `Services` Using Ansible

![Screenshot 2023-06-27 at 2.20.57 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.20.57_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    ---
    - name: 
    	hosts: all
    	become: true
    	tasks:
    		- name: service module
    				service:
    					name: apache2
    					state: started
    					enabled: yes
    ```
    
    The final task is to manage the Apache2 service using the `service` module. There are three `playbook.yml` files that demonstrate starting, stopping, and restarting the service, respectively. The playbooks use the `service` module to perform these tasks and provide a clear demonstration of how to manage services efficiently and effectively.
    
2. `playbook.yml`
    
    ```yaml
    ---
    - name: 
    	hosts: all
    	become: true
    	tasks:
    		- name: service module
    				service:
    					name: apache2
    					state: stopped
    					enabled: no
    ```
    
    Changing the state from started to stopped means that the Apache2 service will be stopped if it is currently running, and it will not be started automatically on system boot. This is useful if you want to temporarily disable the service or perform maintenance on the system.
    
3. `playbook.yml`
    
    ```yaml
    ---
    - name: 
    	hosts: all
    	become: true
    	tasks:
    		- name: service module
    				service:
    					name: apache2
    					state: restarted
    					enabled: yes
    					sleep: 10 apologize for the confusion. According to your recent feedback, the changes made to the third demo playbook are:
    ```
    
    The `state` parameter was set to `restarted` which means that the service will be restarted if it is running, stopped if it is not running, and started again. Additionally, the `sleep` parameter was set to `10` which means that Ansible will wait for 10 seconds after restarting the service.
    

# Managing `Storage` Using Ansible

![Screenshot 2023-06-27 at 2.29.59 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.29.59_PM.png)

![Screenshot 2023-06-27 at 2.30.20 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.30.20_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    ---
    - name: storage 
    	hosts: all 
    	become: true
    	tasks:
    		- name: create lv
    			lvol:
    				vg: rhel 
    				lv: 1v02 
    				size: 1g
    		- name: filesystem 
    			filesystem:
    				fstype: xfs 
    				dev: /dev/rhel/lv02
    		- name: mountpoint 
    			file:
    				path: /mountpoint 
    				state: directory
    		- name: mount 
    			mount:
    				path: /mountpoint 
    				src: /dev/rhel/lv02 
    				fstype: xfs 
    				state: present 
    				opts: defaults 
    				dump: 'O'
    ```
    
    This code is an example of how to use Ansible to manage storage. It creates a logical volume (LV) called `1v02` with a size of `1g` in the volume group `rhel`. Then, it creates a file system with the file system type `xfs` on the logical volume. After that, it creates a mount point at `/mountpoint` and mounts the file system to that mount point with the same file system type and default options.
    
    This playbook demonstrates how easy it is to manage storage using Ansible. By using this code as a reference, you can modify it to suit your specific needs for managing storage with Ansible.
    

# Manage `Network` Configuration Using Ansible

![Screenshot 2023-06-27 at 2.37.32 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.37.32_PM.png)

![Screenshot 2023-06-27 at 2.38.03 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.38.03_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    --- 
    - name: netwrok config
    	hosts: all
    	become: true
    	tasks: 
    		- name: nmcli module
    			nmcli:
    				conn_name: myconn
    				ifname: enp0s31f6
    				type: ethernet
    				ipv4: 192.168.1.1/24
    				gw4: 192.168.1.2
    				dns4: 192.168.1.3
    				state: present 
    ```
    
    This code is an example of how to use Ansible to manage network configuration. The purpose of this code is to create a new connection using the `nmcli` module with the following properties:
    
    - Connection name: `myconn`
    - Interface name: `enp0s31f6`
    - Connection type: `ethernet`
    - IPv4 address: `192.168.1.1/24`
    - IPv4 gateway: `192.168.1.2`
    - DNS server: `192.168.1.3`
    - Connection state: `present`
    
    By using this code as a reference, you can modify it to suit your specific needs for managing network configuration with Ansible.
    
2. `playbook.yml`
    
    ```yaml
    --- 
    - name: netwrok config
    	hosts: all
    	become: true
    	tasks: 
    		- name: nmcli module
    			nmcli:
    				conn_name: myconn
    				ifname: enp0s31f6
    				type: ethernet
    				ipv4: 192.168.1.1/24
    				gw4: 192.168.1.2
    				dns4: 192.168.1.3
    				state: absent
    ```
    
    Changing the `state` parameter to `absent` will remove the connection named `myconn` if it currently exists.
    
3. `playbook.yml`
    
    ```yaml
    ---
    - name: configure firewalld
    	hosts: all
    	become: true
    	tasks:
    		- name: firewalld module 
    			firewalld: 
    				zone: public
    				permanent: no
    				state: enabled 
    				service: http
    ```
    
    The code block you provided is an example of how to configure the `firewalld` module in Ansible. The playbook is named `configure firewalld`, runs on all hosts, and is set to become a privileged user. It contains a single task that uses the `firewalld` module to manage the `http` service in the `public` zone. The `permanent` parameter is set to `no` which means that the changes will not be made permanent, and the `state` parameter is set to `enabled` which means that the `http` service will be enabled in the `public` zone.
    
4. `playbook.yml`
    
    ```yaml
    ---
    - name: configure firewalld
    	hosts: all
    	become: true
    	tasks:
    		- name: firewalld module 
    			firewalld: 
    				zone: public
    				permanent: no
    				state: enabled 
    				source: 192.168.1.1
    ```
    
    The change made to the `configure firewalld` playbook is that the `service` parameter was removed and replaced with the `source` parameter. The `service` parameter was used to manage a specific service, while the `source` parameter is used to manage traffic from a specific source IP address. This means that the playbook will now manage traffic from the IP address `192.168.1.1` in the `public` zone of the `firewalld` module.
    

# `Patch` Management with Ansible

- One of the hardest parts of being a sysadmin is patching systems. a Common Vulnerabilities and Exposure (CVE) notifications or Information Assurance
Vulnerability Alert (IAVA) are quite often, and you need patches.
- Ansible can reduce the time it takes to patch systems by running packaging modules.
- Ansible makes deploying patches easy, fast and management friendly.

## Sample

![Screenshot 2023-06-27 at 2.51.08 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.51.08_PM.png)

![Screenshot 2023-06-27 at 2.51.56 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_2.51.56_PM.png)

- For Debian distribution of linux, we need use `apt` instead of `yum`

## Demo

1. `playbook.yml`
    
    ```yaml
    ---
    - name: install and update services 
    	hosts: all
    	become: true
    	tasks:
    		- name: install and update services
    			apt: 
    				name: 
    					- apache2
    					- firewalld
    				state: latest
    ```
    
    This is a code block that demonstrates how to install and update services using Ansible. The playbook is named `install and update services`, runs on all hosts, and is set to become a privileged user. It contains a single task that uses the `apt` module to manage the `apache2` and `firewalld` services. The `state` parameter is set to `latest` which means that Ansible will ensure that the latest version of these services is installed.
    
2. `playbook.yml`
    
    ```yaml
    ---
    - name: install and update services 
    	hosts: all
    	become: true
    	tasks:
    		- name: install groups of services
    			apt: 
    				name: '@Container Management'
    				state: latest
    ```
    
    The change made is that the task to install and update the `apache2` and `firewalld` services was replaced with a new task to install the `@Container Management` group of services using the `apt` module.
    
3. `playbook.yml`
    
    ```yaml
    --- 
    - name: gather facts
    	hosts: all
    	tasks: 
    		- name: gather installed packages
    			package_facts:
    				manager: auto
    		- name: 
    			debug:
    				var: ansible_facts.packages
    ```
    
    This code block uses the `package_facts` module in Ansible to gather information about installed packages on target hosts. The `ansible_facts.packages` variable contains the list of installed packages and is printed using the `debug` module. This information can be used to identify potential security vulnerabilities or ensure that all required packages are installed.
    
4. `playbook.yml`
    
    ```yaml
    ---
    - name: configure repo
    	hosts: all
    	become: true
    	tasks: 
    		- name: configure apt repo
    			apt_repository:
    				file: mynewrepo
    				name: myrepo
    				description: helloworld
    				baseurl: http://mytest.com/url
    				enabled: no
    				gpgcheck: no
    				state: present
    ```
    
    This is a code block that configures an apt repository using Ansible. The playbook is named `configure repo`, runs on all hosts, and is set to become a privileged user. It contains a single task that uses the `apt_repository` module to manage the repository. The parameters used are as follows:
    
    - `file`: The name of the file to create in the `sources.list.d` directory.
    - `name`: The name of the repository.
    - `description`: A short description of the repository.
    - `baseurl`: The base URL of the repository.
    - `enabled`: Whether the repository is enabled or not.
    - `gpgcheck`: Whether to check the GPG signature of the repository.
    - `state`: Whether the repository should be present or absent.
    
    By using this code as a reference, you can modify it to suit your specific needs for configuring apt repositories with Ansible.
    

# `Hardening` with Ansible

## Hardening

- Systems hardening is a collection of tools, techniques, and best practices to reduce vulnerability in technology applications, systems, infrastructure, firmware, and other
areas.
- The goal of systems hardening is to reduce security risk by eliminating potential attack vectors and condensing the system's attack surface.
- By removing useless programs, accounts functions, applications, ports, permissions, access, etc. attackers and malware have fewer opportunities to gain a foothold within your IT ecosystem.

## Samples

![Screenshot 2023-06-27 at 3.07.55 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.07.55_PM.png)

![Screenshot 2023-06-27 at 3.08.15 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.08.15_PM.png)

![Screenshot 2023-06-27 at 3.09.39 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.09.39_PM.png)

![Screenshot 2023-06-27 at 3.09.49 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.09.49_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    ---
    - name: update all 
    	hosts: all 
    	become: true
    	tasks:
    		- name: patch everything 
    			apt:
    				name: '*'
    				state: latest
    ```
    
    This code block is a demonstration of how to use Ansible to keep all packages installed on target hosts up to date. The playbook is named `update all`, runs on all hosts, and is set to become a privileged user. It contains a single task that uses the `apt` module to manage all packages (`name: '*'`). The `state` parameter is set to `latest` which means that Ansible will update all installed packages to their latest available version.
    
2. `playbook.yml`
    
    ```yaml
    ---
    - name: remove unused software
    	hosts: all 
    	become: true
    	vars:
    		u_software: apache2
    	tasks:
    		- name: remove unused software
    			apt:
    				name: "{{ u_software }}"
    				state: absent 
    ```
    
    This code block is an example of how to remove unused software using Ansible. The playbook is named `remove unused software`, runs on all hosts, and is set to become a privileged user. The variable `u_software` is defined with a value of `apache2`. The task uses the `apt` module to remove the package defined in the `u_software` variable with the `state` parameter set to `absent`. This playbook can be modified to remove other unused software by changing the value of the `u_software` variable.
    
3. `playbook.yml`
    
    ```yaml
    ---
    - name: remove unused software
    	hosts: all 
    	become: true
    	vars:
    		u_software: 
    			- apache2
    			- firewalld
    	tasks:
    		- name: disable unused software
    			service: 
    				name: "{{ item }}" 
    				state: stopped
    				enabled: yes
    			loop: "{{ u_service }}"
    			ignore_errors: yes
    
    vars:
    		u_software: apache2
    tasks:
    		- name: remove unused software
    			apt:
    				name: "{{ u_software }}"
    				state: absent 
    ```
    
    The example code that removes unused software (`apache2`) was replaced with a new task that disables unused software. The unused software is defined as a list of packages (`apache2` and `firewalld`) in the `u_software` variable. The task uses the `service` module to stop and disable the services defined in the `u_software` variable. The `loop` parameter is used to iterate over the list of packages, and the `ignore_errors` parameter is set to `yes` to prevent the playbook from failing if the services are not currently running.
    
4. `playbook.yml`
    
    ```yaml
    ---
    - name: policy
    	hosts: all 
    	become: true
    	tasks: 
    		- name: motd
    			copy: 
    				dest: /etc/motd
    				src: mymessage
    				owner: root
    				group: root
    				mode: 0644
    		- name: banner
    			copy: 
    				dest: "{{ item }}"
    				src: myissue
    				owner: root
    				group: root
    				mode: 0644
    			loop: 
    				- /etc/issue
    				- /etc/issue.net
    ```
    
    This is a code block that demonstrates how to use Ansible to manage system policies. The playbook is named `policy`, runs on all hosts, and is set to become a privileged user. It contains two tasks:
    
    - The first task is named `motd`. It uses the `copy` module to copy a file with the message of the day to `/etc/motd` on all hosts. The `src` parameter specifies the source file (`mymessage`), and the `dest` parameter specifies the destination file (`/etc/motd`). The `owner`, `group`, and `mode` parameters are used to set the file permissions and ownership.
    - The second task is named `banner`. It uses the `copy` module to copy two files with issue banners to `/etc/issue` and `/etc/issue.net` on all hosts. The `src` parameter specifies the source file (`myissue`), and the `dest` parameter specifies the destination file (`{{ item }}`). The `{{ item }}` syntax is used to loop over the two files. The `owner`, `group`, and `mode` parameters are used to set the file permissions and ownership.
    
    By using this code as a reference, you can modify it to suit your specific needs for managing system policies with Ansible.
    
5. `playbook.yml`
    
    ```yaml
    ---
    - name: sudoers
    	hosts: all 
    	become: true
    	tasks: 
    		- name: add sudoers file
    			copy: 
    				dest: /etc/sudoers.d/myadmins
    				src: myadmins 
    				owners: root
    				group: root
    				mode: 0440
    ```
    
    This Ansible playbook creates a sudoers file named `myadmins` and copies it to `/etc/sudoers.d/myadmins` on all hosts. The `owner`, `group`, and `mode` parameters are used to set the file permissions and ownership.
    

# Additional Ansible `Module`

## `Lineinfile`

- This module ensures a particular line is in a file or replace an existing line using a back-referenced regular expression.
- This is primarily useful when you want to change a single line in a file only

![Screenshot 2023-06-27 at 3.30.16 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.30.16_PM.png)

## `find`

- Return a list of files based on specific criteria.
- Similar to the find command within the terminal.
- Real Time search.

![Screenshot 2023-06-27 at 3.31.18 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.31.18_PM.png)

## `Cron`

- Use this module to manage crontab and environment variables entries. This module allows you to create environment variables and named crontab entries, update, or delete them.
- When crontab jobs are managed: the module includes one line with the description of the crontab entry "`#Ansible: <names>`" corresponding to the "name" passed to the module, which is used by future ansible/module calls to find/check the state.
- When environment variables are managed, no comment line is added, but, when the module needs to find/check the state, it uses the "name" parameter to find the environment variable definition line.
- When using symbols such as %, they must be properly escaped.

![Screenshot 2023-06-27 at 3.37.09 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.37.09_PM.png)

## `at`

![Screenshot 2023-06-27 at 3.38.04 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.38.04_PM.png)

## `File`

- Set attributes of files, symlinks or directories.
- Alternatively, remove files, symlinks or directories.

![Screenshot 2023-06-27 at 3.39.21 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.39.21_PM.png)

## `Archive`

- Creates or extends an archive.
- The source and archive are on the remote host, and the archive is not copied to the local host.
- Source files can be deleted after archival by specifying remove=True.

![Screenshot 2023-06-27 at 3.40.50 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.40.50_PM.png)

## `Unarchive`

- The unarchive module unpacks an archive. It will not unpack a compressed file that does not contain an archive.
- By default, it will copy the source file from the local system to the target before unpacking.
- Set remote_src=yes to unpack an archive which already exists on the target.

![Screenshot 2023-06-27 at 3.41.59 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.41.59_PM.png)

## `Fetch`

- This module works like copy, but in reverse
- It is used for fetching files from remote machines and storing them locally in a file tree, organized by hostname.
- Files that already exist at dest will be overwritten if they are different than the sc.

![Screenshot 2023-06-27 at 3.43.21 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.43.21_PM.png)

## `Uri`

![Screenshot 2023-06-27 at 3.44.12 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.44.12_PM.png)

## `get_url`

![Screenshot 2023-06-27 at 3.45.01 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.45.01_PM.png)

## `Script`

- The script module takes the script name followed by a list of space-delimited arguments.
- Either a free form command or md parameter is required, see the examples.
- The local script at path will be transferred to the remote node and then executed.
- The given script will be processed through the shell environment on the remote node.

![Screenshot 2023-06-27 at 3.46.32 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.46.32_PM.png)

## `Synchronize`

- Synchronize is a wrapper around rsync to make common tasks in your playbooks quick and easy.
- It is run and originates on the local host where Ansible is being run.
- Of course, you could just use the command action to call sync yourself, but you also have to add a fair number of boilerplate options and host facts.

![Screenshot 2023-06-27 at 3.47.40 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.47.40_PM.png)

## `Add-host`

- Use variables to create new hosts and groups in inventory for use in later plays of the same playbook.
- Takes variables so you can define the new hosts more fully.

![Screenshot 2023-06-27 at 3.48.26 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.48.26_PM.png)

## `Set_fact`

- This action allows setting variables associated to the current host.
- These variables will be available to subsequent plays during an ansible-playbook run via the host they were set on.
- Set cacheable to yes to save variables across executions using a fact cache. Variables will keep the set_fact precedence for the current run, but will used 'cached fact precedence for subsequent ones.

![Screenshot 2023-06-27 at 3.49.45 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.49.45_PM.png)

## `Git`

![Screenshot 2023-06-27 at 3.50.12 PM.png](7_Automation%20System%20Administration%20Tasks%205cc42527a5ba4ea3be31ef5adf40c99d/Screenshot_2023-06-27_at_3.50.12_PM.png)
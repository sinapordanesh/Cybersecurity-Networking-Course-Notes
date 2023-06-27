# 5_Reducing Complexity Through Modularity

# Importing and Including Playbooks

## Why Import Playbooks?

- Writing long playbooks makes them hard to follow and understand.
- Splitting a large playbook into a series of smaller playbooks means they can be reused in other projects.
- Smaller playbooks are easier to manage and understand.
- Importing a playbooks is a static task which means the imported content is processed before the play starts.
- mporting a playbook can not be included inside a play and they are run in import order from top to bottom.

## Samples

![Screenshot 2023-06-23 at 12.43.23 PM.png](5_Reducing%20Complexity%20Through%20Modularity%20f4750fdda82c43faaa692af10866d6ce/Screenshot_2023-06-23_at_12.43.23_PM.png)

## Demo

- note: this demo is for the redhat linux distribution. something like `httpd` and `yum` are not usable on Debian Linux versions like Kali or Ubuntu
1. setup inventory and ansible.cfg
2. `p /etc/apache2/apache2.conf /hom e/automation/modularity/import/`
3. `install.yml`
    
    ```yaml
    ---
    - name: install httpd
    	host: all
    	tasks: 
    		- name: install httpd 
    				apt: 
    					name: apache2 
    					state: latest 
    ```
    
4. `content.yml`
    
    ```yaml
    ---
    - name: new_content
    	host: all
    	tasks: 
    		- name: create path
    			file: 
    				path: /website/html
    				state: directory
    		- name: template placement 
    			template: 
    				src: template
    				dest: /website/html/index.html 
    ```
    
5. `httpd.yml`
    
    ```yaml
    ---
    - name: apache2 configure
    	hosts: all
    	tasks: 
    		- name: copy apache2 conf
    			copy: 
    				src: apache2.conf
    				dest: /etc/httpd/conf/apache2.conf
    			notify: restart
    	handlers: 
    		- name: restart
    			service:
    				name: apache2 
    				state: restarted
    ```
    
6. `selinux.yml`
    
    ```yaml
    ---
    - name: selinux fix
    	hosts: all
    	tasks: 
    		- name: set selinux
    			command: semanage fcontext -a -t httpd_sys_content_t "/website(/.*)?"
    		- name: restore con
    			command: restorecon -R /website 
    ```
    
7. `template`
    
    ```yaml
    Hi my name is {{ ansible_facts['hostname']}}
    ```
    
8. `playbook.yml`
    
    ```yaml
    --- 
    - name: import install
    	import_playbook: install.yml
    - name: import content
    	import_playbook: content.yml
    - name: import selinux
    	import_playbook: selinux.yml
    - name: import httpd 
    	import_playbook: httpd.yml
    ```
    

# Importing and Including Tasks

## Why Import/Include Tasks?

- You can import/include tasks in a play from a task file.
- When using the import function tasks are imported within the playbook when the playbook is parsed.
- When you using the import function you cannot use loops.
When using the import function in conjunction with a conditional statement then the conditional statement will apply to all tasks imported.
- When using the include function tasks are added to the play when that point is reached while running the play.
- When using the include function in conjunction with conditional statements then the conditional statement will decide if the tasks are included or not.
- When using the include function vou cannot notify any handler from an included task file.

## Samples

![Screenshot 2023-06-23 at 1.27.44 PM.png](5_Reducing%20Complexity%20Through%20Modularity%20f4750fdda82c43faaa692af10866d6ce/Screenshot_2023-06-23_at_1.27.44_PM.png)

## Demo

1. `inventory` and `ansible.cfg`
2. `create.yml`
    
    ```yaml
    ---
    - name: 
    	user: 
    		name: "{{ username }}"
    		state: present 
    ```
    
3. `template.yml`
    
    ```yaml
    ---
    - name: place templatefile 
    	template: 
    		src: "{{ templatefile}}"
    		dest: "/home/{{ username }}/myfile"
    ```
    
4. `template`
    
    ```yaml
    Place by Ansible on {{ ansible_facts['hostname'] }} !
    ```
    
5. `playbook.yml`
    
    ```yaml
    ---
    - name: create user and place template 
    	hosts: all
    	tasks: 
    		- name: include_task
    			include_tasks: create.yml
    			vars:
    				username: user1
    		- name: place template 
    			include_tasks: template.yml
    			vars: 
    				username: user1
    ```
    

# Testing Specific Hosts

- Until now we just used one object to tell Ansible who it should target within the inventory.
- The group "all" contains all hosts within the inventory and the group "ungrouped" contains all servers not present within a group.
- We can better specify who we are targeting through the use of wildcards and lists
- Elements within lists are comma separated.
- Elements can be excluded by using the exclamation point in front of the host pattern.

## Sample

![Screenshot 2023-06-23 at 1.37.01 PM.png](5_Reducing%20Complexity%20Through%20Modularity%20f4750fdda82c43faaa692af10866d6ce/Screenshot_2023-06-23_at_1.37.01_PM.png)

## Demo

1. `inventory` and `ansible.cfg`
    
    `inventory`
    
    ```yaml
    servera 
    serverb
    192.168.1.1
    192.168.1.2
    192.168.1.3
    192.168.1.4
    [justservera]
    servera 
    [justserverb]
    serverb
    ```
    
    `ansible all —list-hosts`
    
    `ansible ungrouped —list-hosts`
    
    `ansible 192.168* —list-hosts`
    
    `ansible servers* —list-hosts`
    
2. `playbook.yml`
    
    ```yaml
    ---
    - name: test host patterns
    	hosts: all, !192.*, !servera
    	tasks : 
    		- name: debug
    			debug: 
    				msg: "{{ ansible_facts['hostname'] }}"
    ```
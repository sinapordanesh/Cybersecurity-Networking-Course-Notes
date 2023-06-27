# 4_Using Variables, Loops, and Conditionals Within Playbooks

# Ansible Variables

- Just like in programming languages, variables in Ansible are used to store a value.
- Variables provide flexibility in Playbooks, templates and inventories.
- Built-in variables can be used to provide system information.
- Variables can be defined in various places.
- Variable names should only contain letters, numbers or underscores, any combination of these is fine.

![Screenshot 2023-06-22 at 10.52.08 AM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_10.52.08_AM.png)

## Samples

- In playbook file

![Screenshot 2023-06-22 at 10.52.35 AM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_10.52.35_AM.png)

- In an inventory file

![Screenshot 2023-06-22 at 10.53.18 AM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_10.53.18_AM.png)

## Magic Variables

![Screenshot 2023-06-22 at 10.54.06 AM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_10.54.06_AM.png)

## Ansible Facts

- Variables automatically discovered when Ansible connects to a managed host.
- They contain information on the managed host such as hostname, IP Address, Memory etc.
- Can be used like any other variable.
- Useful to know what state a managed host is in and determine actions.
- The have parents and children which can be clearly seen.

![Screenshot 2023-06-22 at 10.54.56 AM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_10.54.56_AM.png)

1. `ansible servera -m setup`: This command runs the `setup` module on the `servera` host, which gathers information about the system and saves it as Ansible Facts. This is useful for debugging and understanding the state of the system.
2. `ansible. facts['fadn']`: This command tries to access a fact named `fadn` from the Ansible Facts. However, `fadn` is not a valid fact name, and the syntax of the command is incorrect. Please provide more context on what you intended to do with this command.
3. `ansible facts[*default ipv4'| ('addresses']`: This command is also not valid. It seems like you are trying to access the default IPv4 address of a host, but the syntax is incorrect. The correct syntax to access the default IPv4 address is `ansible_facts['default_ipv4']['address']`.
4. `name: playbook gather facts: yes/no`: This is not a command, but a YAML key for the `gather_facts` option in an Ansible playbook. It specifies whether to gather facts (system information) from the hosts before running tasks. If `gather_facts` is set to `yes`, Ansible will run the `setup` module on the host to gather information and save it as Ansible Facts.

## Demo

1. make a dir called `variables` 
2. create inventory and configuration files:
    1. `inventory`
    
    ```yaml
    servera
    serverb
    [servers]
    servera
    serverb
    ```
    
    b.  `ansible.cfg`
    
    ```yaml
    [defaults]
    remote_user= automation
    inventory= /home/automation/variables/inventory 
    [privilege escalation]
    become= true 
    become_metho d= sudo 
    become_user= root 
    become_ask_pass= false
    ```
    
3. create a `playbook.yml`
    1. Internal variables 
        
        `playbook.yml`
        
        ```yaml
        ---
        - name: myplay 
        	hosts: servera 
        	  become: true
          become_user: root
        	vars:
        		user: variableuser 
        		state: absent
        	tasks:
        		- name: create user 
        			user:
        				name: "{{ user }]" 
        				state: "{{ state }"
        ```
        
    
    b. External vairalbes 
    
    `playbook.yml`
    
    ```yaml
    ---
    - name: myplay 
    	hosts: servera 
    	become: true
      become_user: root
    	vars_files:
    		vars/variable.yml
    	tasks:
    		- name: create user 
    			user:
    				name: "{{ user }]" 
    				state: "{{ state }"
    ```
    
    `variables.yml`
    
    ```yaml
    user: testfile
    state: present 
    ```
    
    c. Internal **Array** of variables 
    
    `playbook.yml`
    
    ```yaml
    ---
    - name: myplay 
    	hosts: servera 
    	become: true
      become_user: root
    	vars:
    		testarray:
    			firstarray:
    				name: first 
    				uid: 1011 
    			secondarray:
    				name: second 
    				uid: 1012
    	tasks:
    		- name: create user 
    			user:
    				name: "{{ testarray.firstarray.name }}" 
    				uid: "{{ testarray.firstarray.uid}}"
    				state: present 
    ```
    
4. Run the code
    
    ```yaml
    ansible-playbook --syntax-check playbook.yml
    ansible-playbook playbook.yml
    ansible servera -m command -a 'cat /etc/passwd'
    ```
    

### Automate Ansible facts gathering

- List all facts:
    
    `ansible servera -m setup > facts.yml`
    
- `playbookfacts.yml`
    
    ```yaml
    ---
    - name: display facts 
    	hosts: serverb 
    	tasks:
    		- name: show facts 
    			debug:
    				msg: The fqdn is {{ ansible_facts['fqdn'] }}
    ```
    

# Ansible Loops

- Used to perform the same task on a set of data without writing it multiple times.
- Ansible supports loops over datasets.
- Ansible also supports loops over hashes

## Sample

![Screenshot 2023-06-22 at 4.28.52 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_4.28.52_PM.png)

![Screenshot 2023-06-22 at 4.29.14 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_4.29.14_PM.png)

## Demo

1. `playbook.yml`
    
    ```yaml
    - name: loops 
    	hosts: all 
    	become: true
      become_user: root
    	tasks:
    		- name: restart services 
    			service:
    				name: "{{ item }}" 
    				state: restarted
    			loop:
    				-firewalld
    				- crond
    ```
    
2. `playbook.yml`
    
    ```yaml
    - name: loops 
    	hosts: all 
    	become: true
      become_user: root
    	vars: 
    		services:
    			- crond
    			- firewalld
    	tasks:
    		- name: restart services 
    			service:
    				name: "{{ item }}" 
    				state: restarted
    			loop: "{{ services }}"
    ```
    
3. `playbook.yml`
    
    ```yaml
    - name: loops 
    	hosts: all 
    	become: true
      become_user: root
    	tasks:
    		- name: restart services 
    			user: 
    				name: "{{ item.name }}" 
    				uid: "{{ item.uid   }}" 
    			loop:
    				- name: loopuser1
    					uid: 1015
    				- name: loopuser2
    					uid: 1016
    ```
    

# Ansible Conditional Statements

## Conditions

- Ansible supports conditional evaluations before executing a specific task on the target hosts.
- If the set condition is true, Ansible will go ahead and perform the task.
- If the condition is not true Ansible will skip the specified task.

### Samples

![Screenshot 2023-06-22 at 5.03.24 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_5.03.24_PM.png)

## Handlers

- Handlers are tasks which are executed only if they have been notified by another task.
- They are written in a separate section of the playbook and are notified by name
- Notification only happens when a change is reported by the task charged with notifying the handler.
- If the task does not report the change then the handler will not be notified.

### Samples

![Screenshot 2023-06-22 at 5.04.56 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_5.04.56_PM.png)

## Blocks

![Screenshot 2023-06-22 at 5.05.13 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_5.05.13_PM.png)

## Demo

### Conditionals

- `palybookconditionals.yml`
    
    ```yaml
    ---
    - name: conditionals
    	hosts: all
    	become: true
      become_user: root
    	vars: 
    		service: apache2 
    	tasks: 
    		- name: install a service 
    			apt:
    				name: "{{ service }}"
    				state: latest
    			when: service is defined 
    ```
    
- `palybookconditionals.yml`
    
    ```yaml
    ---
    - name: conditionals
    	hosts: all
    	become: true
      become_user: root
    	tasks: 
    		- name: create a new file
    			copy:
    				content: this is servera
    				dest: /home/automation/conditionals
    			when: ansible_hostname == "servera"
    ```
    

### Handlers

- `playbookhandler.yml`
    
    ```yaml
    ---
    -name: handlers
    	hosts: all
    	become: true
      become_user: root
    	tasks:
    		- name: add new firewall rule
    			firewalld:
    				service: http
    				state: enabled 
    				permanent: true 
    			notify: restart_firewall
    	handlers:
    		- name: restart_firewall
    			service:
    				name: firewalld
    				state: restarted
    ```
    

### Blocks

- `playbookblocker.yml`
    
    ```yaml
    ---
    - name: use of blockers
    	hosts: all
    	tasks:
    		- name: install apache2
    			block:
    				- name: start apache2
    					service:
    						name: apache2
    						state: started
    			rescue:
    				- name: install apache2
    					apt:
    						name: apache2
    						state: latest
    ```
    

# Ansible Templates

## Templates

- Templates make managing files easier.
- Templates make customization of files for the managed host easier.
- They are written in Jinja2 syntax.
- Templates are deployed using the template module.
- Templates can use both Ansible facts and variables.
- They support loops and conditionals

## Samples

![Screenshot 2023-06-22 at 5.32.53 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_5.32.53_PM.png)

![Screenshot 2023-06-22 at 5.39.38 PM.png](4_Using%20Variables,%20Loops,%20and%20Conditionals%20Within%20%20860bceb6ce8841579b3f5451e49cf61a/Screenshot_2023-06-22_at_5.39.38_PM.png)

## Demo

A. `playbooktemplate.yml`

```yaml
--- 
- name: templates
	hosts: all
	tasks: 
		- name: template placement
			template: 
				src: /home/automation/templates/template
				dest: /home/automation/templates 

```

1. `template`
    
    ```yaml
    My hostname is {{ ansible_facts['hostname'] }}
    ```
    
2. `template`
    
    ```yaml
    {% for host in groups['justservera'] %} 
    {{ hostvars[host]['a nsible_facts']['hostname'] }}
    {% endfor %}
    ```
    
3. `template`
    
    ```yaml
    {% if ansible_facts['hostname'] in groups['justservera'] %}
    {{ ansible_facts['hostname'] }} is in the group justservera
    {% endif %}
    {% if ansible_facts['hostname'] not in groups['justservera'] %}
    i'm not in the group
    {% endif %}
    ```
    

B. `playbooktemplate.yml`

```yaml
--- 
- name: templates
	hosts: all
	vars: 
		user: sina
		comment: mycomment
		server: serverc
	tasks: 
		- name: template placement
			template: 
				src: /home/automation/templates/template
				dest: /home/automation/templates 

```

`template`

```yaml
I will create a new user called {{ user }} 
This user shall the comment {{ comment }}
The user is place on the {{ server }}   
```

- **run the code:**
    
    `ansible-playbook playbooktemplate.yml`
    
- **check the result:**
    
    `ansible servera -m command -a 'cat /home/automation/templates'`
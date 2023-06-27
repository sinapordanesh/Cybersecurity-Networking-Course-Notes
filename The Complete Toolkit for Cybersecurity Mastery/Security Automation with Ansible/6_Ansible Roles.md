# 6_Ansible Roles

# What is an Ansible Role?

- Playbooks can become complex when they are needed to configure multiple systems with multiple tasks for each system.
- Ansible lets you organize tasks in a directory structure called a Role
- In this configuration, playbooks invoke roles instead of tasks.
- Roles allow you to collect templates, static files, and variables along with your tasks in one structured format.
- Roles allow you to break down a complex playbook into separate, smaller chunks that can be coordinated by a central entry point.
- If main .yml exists in a directory, its contents will be automatically added to the playbook that calls the role.
- When you use a roles section to import roles into a play, the roles will run first, before any tasks that you define for that play.

## Role Directories

![Screenshot 2023-06-27 at 12.11.16 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.11.16_PM.png)

![Screenshot 2023-06-27 at 12.11.34 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.11.34_PM.png)

## Role Placement

- Ansible looks for a directory called "roles" in the same path where your playbook resides.
- If Ansible cannot find the "roles" directory it will look in the paths specified in the Ansible Configuration file under the "`roles_path`" setting.
- Role paths can be specified in order separated by a colon.
- If the "`roles_path`" is not specified in the configuration file then it will look in the default paths.
- `~/.ansible/roles:/us/share/ansible/roles:/etc/ansible/roles`

# Using Ansible Roles Within Playbooks

## Sample

![Screenshot 2023-06-27 at 12.14.29 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.14.29_PM.png)

![Screenshot 2023-06-27 at 12.14.52 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.14.52_PM.png)

## Demo

1.  Create the following tree
    
    ![Screenshot 2023-06-27 at 12.17.04 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.17.04_PM.png)
    
2. `/roles/ansible.cfg
/roles/inventory
/roles/playbooks.yml` :
    
    ```yaml
    ---
    - name: role apache2
      hosts: all
      roles:
        - roles
    ```
    
3. `/roles/roles/handlers/main.yml`
    
    ```yaml
    ---
    # Handlers file for roles/
    - name: start apache2
      service:
        name: "{{service}}"
        state: restarted
    ```
    
4. `/roles/roles/tasks/main.yml` 
    
    ```yaml
    ---
    # Tasks file for roles/
    - name: install apache2
      apt:
        name: "{{service}}"
        state: "{{state}}"
      notify: start apache2
    - name: content
      template:
        src: content
        dest: /var/www/html/index.html
    ```
    
5. `/roles/roles/templates/content`
    
    ```
     Hello my name is {{ ansible_facts['hostname'] }}
    ```
    
6. `/roles/roles/vars/main.yml`
    
    ```yaml
    ---
    # vars file for roles/
    service: apache2
    state: present
    ```
    

# Obtaining Roles and Using Them
Within Playbooks

## Ansible Galaxy

- Ansible Galaxy is a large public repository of Ansible roles
- It contains thousands of Ansible roles.
- It has a searchable database that helps Ansible users identify roles that they need.
- Ansible Galaxy includes links to documentation and videos for new Ansible users and role developers.
- The link is: https://galaxy.ansible.com
- The ansible-galaxy command line tool can also be used to search, display, install, remove, and list roles.
- Personalizing a role is done through the use of variables.

## Sample

![Screenshot 2023-06-27 at 12.49.57 PM.png](6_Ansible%20Roles%2079de3bc790af448bbedf7b54b4b7e05b/Screenshot_2023-06-27_at_12.49.57_PM.png)

## Demo

- commands:
    - `ansible-galaxy search <service>`
    - `ansible-galaxy info <role name>`
    - `ansible-galaxy install <role name>`
    - `ansible-galaxy list`
    - `ansible-galaxy remove <role name>`
- After installation of a role, just put the name of that role on your playbook and run the playbook. E.g:
    - First install the following role:
        
        `ansible-galaxy install geerlingguy.mysql`
        
    - Change the `playbook.yml` like this:
        
        ```yaml
        ---
        - name: role apache2
          hosts: all
          roles:
            - geerlingguy.mysql
        ```
        
    - Rune the play book:
        
        `ansible-playbook playbool.yml`
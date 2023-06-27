# 8_Ansible Tower

# What is Ansible Tower?

- Now known as Ansible Automation Controller.
- Ansible Tower is the enterprise version of Ansible, and it helps organizations and teams scale quickly and effectively.
- There is a cost associated with adopting it, installing it, and getting the software up and running in your environments.
- Ansible Tower offers a user-friendly web user interface.
- Tower allows sysadmins to demonstrate the value and power of automation.
- It is easier to train and demonstrate that leads to quicker acceptance and buy-in.
- Ansible Tower requires a license to use the software.
- There is a trial license available for free.

![Screenshot 2023-06-27 at 3.52.45 PM.png](8_Ansible%20Tower%202229a13c8704495fa9687d6b65aae93a/Screenshot_2023-06-27_at_3.52.45_PM.png)

# Deploying Ansible Tower

## Architecture

- Single machine with Integrated Database
- Single machine with Remote Database.
- Multi-machine cluster with Remote Database.
- OpenShift pod with Remote Database.

## Requirements

- Red Hat Enterprise Linux or CentOs
- 2 CPUs
- 4 GB RAM
- 40 GB Storage

## Installing Ansible Tower

- You have to use Ansible 2.8 or greater on RHEL 8 to install Tower.
- The Ansible Tower installation has to run from an internet-connected machine in order to pull down the applicable software repositories
- Download and then extract Ansible Tower to your control machine.
- Once the setup script finishes, you will be able to access your Tower instance via the web browser.
- Type your control machine's IP address into the browser and hit Enter.
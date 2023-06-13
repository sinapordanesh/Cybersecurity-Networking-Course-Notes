# 2_Setting Up a Lab for Network Penetration Testing

# Learning Objectives

- Setting up a hypervisor to create a virtual lab environment
- Setting up virtual networking to ensure your attacker machine (Kali Linux) has connectivity with vulnerable machines
- Deploying and getting started with Kali Linux
- Creating vulnerable host machines
- Implementing vulnerable web applications
- Setting up a vulnerable wireless network

## Technical Requirements

- A hypervisor - Oracle VM VirtualBox
- 
- Oracle VirtualBox Extension Pack
- 8 GB RAM or greater
- Quad core CPU or greater
- 200 GB free space on HDD/SSD
- Internet connection

**Metasploitable** is a virtual machine that has been intentionally designed with vulnerabilities to practice penetration testing. It is a popular target for penetration testing due to the various vulnerabilities it contains, making it an excellent tool for practicing and learning penetration testing.

![Screenshot 2023-04-18 at 4.24.53 PM.png](2_Setting%20Up%20a%20Lab%20for%20Network%20Penetration%20Testing%2083192283e7a04bfe9e84736c50fc83e8/Screenshot_2023-04-18_at_4.24.53_PM.png)

To create a virtual network on Kali Linux installed on Parallels VM, follow these steps:

1. Open Parallels Desktop and start the Kali Linux virtual machine.
2. Click on "Devices" in the menu bar and select "Network 1" and choose "Shared Network".
3. Click on "Devices" again and select "Network 2" and choose "Host-Only".
4. Open the Terminal in Kali Linux and type the following comm  and: `sudo nano /etc/network/interfaces`
5. Add the following lines to the file:

```
auto eth1
iface eth1 inet dhcp

```

1. Save the file and exit.
2. Type the following command in the Terminal: `sudo ifup eth1`
3. Verify that the network is working by typing the following command: `ping google.com`

Your Kali Linux virtual machine should now be connected to a virtual network.

## Set up Vulnerable Host Machine

# Metasploitable 2

## Metasploitable 2 and its installation on VirtualBox

Metasploitable 2 is an intentionally vulnerable Linux virtual machine that is designed for testing security tools and demonstrating common vulnerabilities. It is useful for practicing and learning penetration testing techniques.

To install Metasploitable 2 on VirtualBox, follow these steps:

1. Download the Metasploitable 2 virtual machine image from the Rapid7 website.
2. Open VirtualBox and click on "New" to create a new virtual machine.
3. Give the virtual machine a name and select "Linux" as the type and "Ubuntu (32-bit)" as the version.
4. Set the amount of RAM to at least 512 MB, and create a new virtual hard disk with at least 8 GB of space.
5. On the "Storage" tab, click "Controller: IDE" and then click the "Add" button to add a new CD/DVD drive.
6. Select "Choose/Create a disk image" and then navigate to the location where you downloaded the Metasploitable 2 virtual machine image.
7. Click "Start" to launch the virtual machine.

Once the virtual machine is running, you can use it to practice network penetration testing techniques.

Here are some useful commands that can be used in Metasploitable 2:

- `nmap`: A tool for network exploration and security auditing.
- `msfconsole`: The main interface for Metasploit Framework, a tool used for developing and executing exploit code against a remote target machine.
- `search`: A Metasploit command used to search for a specific exploit or module.
- `use`: A Metasploit command used to select an exploit or module for use.
- `set`: A Metasploit command used to set options for an exploit or module.
- `exploit`: A Metasploit command used to execute an exploit against a target machine.
- `meterpreter`: A payload that can be used to gain remote access to a target machine.

These are just a few of the many commands that can be used in Metasploitable 2.

Username: `msfadmin`

Password: `msfadmin`

Shutting down: `sudo halt`

# Metasploitable 3

## Metasploitable 3 and its installation using Vagrant

Metasploitable 3 is a virtual machine designed to test security tools and demonstrate common vulnerabilities. It is useful for practicing and learning penetration testing techniques. It is built on Ubuntu 14.04 and is designed to work with Vagrant, a tool for building and managing virtual machine environments.

To install Metasploitable 3 using Vagrant on Windows, follow these steps:

1. Download and install VirtualBox from the official website.
2. Download and install Vagrant from the official website.
3. Open Command Prompt on your Windows machine.
4. Change the current directory to where you want to create the virtual machine.
5. Run the following command to download and install the Metasploitable 3 box:

```powershell
vagrant plugin install vagrant-reload
vagrant plugin install vagrant-vbguest
vagrant box add rapid7/metasploitable3-win2k8

(Then select the appropriate VM which you are using)
```

Then, go to C drive → Users → ‘username’ → .vagrant.d → boxes

You’ll find the downloaded package (”rapid7-VAGRANTSLASH-metasploitable3-win2k8”). Rename it to “metasploitable3-win2k8”. Then:

```powershell
cd C:\Users\”username”\.vagrant.d\boxes`
vagrant init metasploitable3-win2k`
vagrant up`
```

This will create a virtual machine on the VirtualBox. 

Password for both users will be: `vagrant`

## Vulnerable web application

`curl -fsSL [https://download.docker.com/linux/debian/gpg](https://download.docker.com/linux/debian/gpg) | gpg --dearmor | sudo tee /usr/share/keyrings/docker-archive-keyring.gpg >/dev/null`

This command downloads a GPG key from the Docker website via curl and then runs the `gpg` command with the `--dearmor` flag to convert the GPG key to a binary format. The binary format is then piped to `sudo tee` command which writes the output to `/usr/share/keyrings/docker-archive-keyring.gpg` file. The `>/dev/null` at the end of the command prevents any output from being displayed on the console.

This command is used to add the GPG key to the system, which is required to verify the Docker packages before installation.

`echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian buster stable' | sudo tee /etc/apt/sources.list.d/docker.list`

`sudo apt update`

`sudo apt install -y docker-ce docker-ce-cli [containerd.io](http://containerd.io/)`

`sudo docker pull bkimminich/juice-shop`

`sudo docker run --rm -p 3000:3000 bkimminich/juice-shop`
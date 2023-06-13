# 4_Linux Administration and Operation in the Cloud

# Understanding the Linux File System

![Screenshot 2023-06-03 at 11.31.24 AM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_11.31.24_AM.png)

`man hier` is a command used to display the manual page for the "hier" file, which provides a description of the Linux file system hierarchy.

The root directory is the top-level directory of the Linux file system hierarchy. It is represented by a forward slash (/). All other directories and files in the file system are contained within the root directory.

- `/bin`: Essential binary executable files that are required by the system and users, such as basic commands like `ls`, `cat`, and `cp`.
- `/boot`: Files and data needed during the boot process, such as the kernel and bootloader configuration files.
- `/dev`: Contains device files that represent hardware components connected to the system, such as hard drives and USB devices.
- `/etc`: Configuration files and directories for the system and **applications**.
- `/home`: Home directories for individual users on the system.
- `/lib`: Libraries required for binaries in `/bin` and `/sbin`.
    - `lib/python3.*/site-packages`: Contains third-party Python modules installed on the system.
- `/media`: Mount point for removable media devices like USB drives and CDs.
- `/mnt`: Mount point for temporary file systems.
- `/opt`: Optional application software packages.
- `/proc`: Contains information about running processes and system resources.
- `/root`: Home directory for the root user on the system.
- `/run`: Information about the running system since last boot.
- `/sbin`: Essential binary executable files that are required by the system and system administrators, such as system maintenance commands and network administration utilities.
- `/srv`: Data for services provided by the system.
- `/sys`: Contains information about devices, drivers, and some kernel settings.
- `/tmp`: Temporary files created by the system and users.
- `/usr`: Contains programs, libraries, and documentation for all user-related programs.
- `/var`: Contains files and directories that are expected to change in size and content as the system is running.

# Creating Files and Directories

The `ls -al` command can be used to list all files and directories in the current directory, including hidden files.

The `touch` command is used to create a new file in the current directory or update the modification time of an existing file. To create a new file called "example.txt" in the current directory, use the command `touch example.txt`.

![Screenshot 2023-06-03 at 11.56.15 AM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_11.56.15_AM.png)

# User Management

![Screenshot 2023-06-03 at 11.56.53 AM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_11.56.53_AM.png)

The `adduser` command is used to create a new user account on the system. To create a new user account with the username "newuser", use the command `sudo adduser newuser`. You will be prompted to set a password and other user information.

The `/etc/passwd` file contains user account information for the system. Each line in the file describes a user account, and consists of seven fields separated by colons (`:`). The fields are:

1. **Username:** The user's login name.
2. **Password:** An "x" in this field indicates that the password for the account is stored in the `/etc/shadow` file. A "*" in this field indicates that the account has no password.
3. **User ID (UID):** A unique numeric identifier for the user.
4. **Group ID (GID):** The primary group ID for the user.
5. **Comment:** A brief description of the user (can be empty).
6. **Home directory:** The full path to the user's home directory.
7. **Login shell:** The command or shell used when the user logs in to the system.

Note that the password field is usually replaced with an "x", indicating that the actual password is stored in the `/etc/shadow` file. The `/etc/passwd` file itself is readable by all users on the system, while the `/etc/shadow` file is only readable by root.

The `sudo passwd akira` command is used to set a new password for the user account "akira". You will be prompted to enter the new password twice. Note that you must have administrative privileges (sudo) to change another user's password.

The `sudo usermod -c "Sina" akira` command is used to change the comment field for the user account "akira" to "Sina". The comment field is the sixth field in the `/etc/passwd` file, and is usually used to provide additional information about the user. The `-c` option is used to specify the new comment for the user account. Note that you must have administrative privileges (sudo) to modify user accounts.

Use `su - sina` to switch to the user account "sina" and start a new login session as that user.

![Screenshot 2023-06-03 at 12.06.22 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.06.22_PM.png)

# Group Management in Linux

![Screenshot 2023-06-03 at 12.07.17 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.07.17_PM.png)

Here are some group commands in Linux:

- `groupadd`: Used to create a new group on the system.
- `groupdel`: Used to delete a group from the system.
- `groupmod`: Used to modify an existing group on the system.
- `newgrp`: Used to change the current group to another group, if the user is a member of that group.
- `groups`: Used to display the groups that the current user is a member of.

The `sudo groupmems -a sina -g eng` command is used to add the user "sina" to the "eng" group. This command modifies the `/etc/group` file to add the user to the specified group. Note that you must have administrative privileges (sudo) to modify group membership.

The `sudo chgrp eng /usr/local/eng` command is used to change the group ownership of the directory `/usr/local/eng` to the "eng" group. This command modifies the `/etc/group` file to give the "eng" group ownership of the specified directory. Note that you must have administrative privileges (sudo) to modify group ownership.

The command `sudo chown -R root:engineering /usr/local/eng` is used to change the ownership of the directory `/usr/local/eng` to the user "root" and the group "engineering". The `-R` option is used to apply the ownership change recursively to all files and directories within the `/usr/local/eng` directory.

![Screenshot 2023-06-03 at 12.16.20 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.16.20_PM.png)

# Software Management in Linux

![Screenshot 2023-06-03 at 12.17.25 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.17.25_PM.png)

`yum repolist` is a command used to list the available YUM repositories on a Linux system. This can be useful for checking which repositories are enabled, what packages are available from those repositories, and what versions of those packages are available. Note that this command requires administrative privileges (sudo) to run.

The `yum search cowsay` command is used to search for the package "cowsay" in the YUM repositories on a Linux system.

The `yum info cowsay` command is used to display detailed information about the "cowsay" package, including its version, dependencies, and other information. Note that this command requires administrative privileges (sudo) to run.

The `sudo yum install cowsay` command is used to install the "cowsay" package from the YUM repositories on a Linux system. Note that this command requires administrative privileges (sudo) to run.

The command `sudo yum remove cowsay` is used to remove the "cowsay" package from the system. Note that this command requires administrative privileges (sudo) to run.

The `yum check-update` command is used to check for updates to all installed packages on the system. Note that this command requires administrative privileges (sudo) to run.

The `yum update` command is used to update all installed packages on a Linux system. Note that this command requires administrative privileges (sudo) to run.

![Screenshot 2023-06-03 at 12.26.14 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.26.14_PM.png)

# Monitoring a Linux Server

![Screenshot 2023-06-03 at 12.26.53 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.26.53_PM.png)

`top` command shows system resource usage and process information, sorted by CPU or memory usage. Use `q` to exit. Requires sudo.

The `top` command provides the following system resource information in a list:

- Process ID (PID)
- Process owner
- CPU usage percentage
- Memory usage percentage
- Virtual memory usage percentage
- Resident set size (RSS) in kilobytes (KB)
- Process status (running, sleeping, zombie, etc.)
- Process start time
- Command name or program name

The `vmstat 1 5` command is used to display virtual memory statistics for a Linux system. The `1` specifies the sampling interval in seconds, and the `5` specifies the number of samples to display. The command provides the following information:

- Processes: The number of processes running on the system.
- r: The number of processes in the run queue (waiting for CPU time).
- b: The number of processes in uninterruptible sleep (usually waiting for I/O).
- swpd: The amount of virtual memory used.
- free: The amount of idle memory.
- buff: The amount of memory used for buffering I/O operations.
- cache: The amount of memory used for caching file system data.
- si: The amount of memory swapped in from disk per second.
- so: The amount of memory swapped out to disk per second.
- bi: The number of blocks received from a block device (hard disk, CD-ROM, etc.) per second.
- bo: The number of blocks sent to a block device per second.

![Screenshot 2023-06-03 at 12.38.15 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.38.15_PM.png)

# Networking in Linux

![Screenshot 2023-06-03 at 12.39.27 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.39.27_PM.png)

The `systemctl status network.service` command is used to view the status of the network service on a Linux system. This command displays information about the current state of the service, including whether it is running or stopped, any errors or warnings, and the time it was last started or stopped. Note that this command requires administrative privileges (sudo) to run

The `ip addr list` command is used to display information about network interfaces on a Linux system, including their IP addresses and other network configuration settings. Note that this command requires administrative privileges (sudo) to run.

To show the IP address and other configuration settings for the "eth0" network interface, use the command `ip addr show dev eth0`. This command displays information about the specified network interface, including its IP address, subnet mask, and MAC address.

The `ip route list` command is used to display the routing table for a Linux system. This command shows the available network routes, including the destination IP address, subnet mask, and gateway address for each route. Note that this command requires administrative privileges (sudo) to run.

The `ss -s` command is used to display summary statistics for network connections on a Linux system. This command provides the following information:

- Total number of sockets (both TCP and UDP)
- Number of sockets in each state (established, closed, etc.)
- Number of packets sent and received
- Number of errors

Note that this command requires administrative privileges (sudo) to run.

The `ss -tnp` command is used to display a list of TCP sockets on a Linux system, including their state and the process ID (PID) associated with each socket. This can be useful for troubleshooting network issues or identifying which processes are using network resources. Note that this command requires administrative privileges (sudo) to run.

The command `ss -tnlp` is used to display a list of TCP sockets on a Linux system, including their state, the local and remote IP addresses and ports, and the process ID (PID) and name associated with each socket. Note that this command requires administrative privileges (sudo) to run.

![Screenshot 2023-06-03 at 12.49.52 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.49.52_PM.png)

# Manage Services in Linux with System

![Screenshot 2023-06-03 at 12.50.51 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_12.50.51_PM.png)

## `cat /etc/systemd/system/multi-user.target.wants/postfix.service`

The command  `cat /etc/systemd/system/multi-user.target.wants/postfix.service` displays the contents of a systemd unit file used to manage the Postfix mail transport agent on a Linux system. The file specifies settings, commands, and the service type for the Postfix service. It also specifies that the service should start after the `syslog.target` and `network.target` services have started, and should be enabled for the `multi-user.target` run level. Overall, this file is important for managing the Postfix service and provides the necessary configuration and commands for starting, stopping, and reloading the service.

## **`systemctl list-unit-file`**

The `systemctl list-unit-files` command is used to display a list of all installed systemd unit files on a Linux system. This can be useful for checking which services are available and which are enabled or disabled. Note that this command requires administrative privileges (sudo) to run.

Here is an example output of the command:

```
UNIT FILE                                  STATE
proc-sys-fs-binfmt_misc.automount           static
dev-hugepages.mount                        static
dev-mqueue.mount                           static
proc-sys-fs-binfmt_misc.mount              static
sys-fs-fuse-connections.mount              static
sys-kernel-config.mount                    static
sys-kernel-debug.mount                     static
tmp.mount                                  disabled
var-lib-nfs-rpc_pipefs.mount                static
brandbot.path                              enabled
brandbot.service                           enabled

```

In this example, the `brandbot.path` and `brandbot.service` unit files are enabled and will run on startup, while the `tmp.mount` unit file is disabled and will not run on startup.

## `systemctl status postfix.service`

A command to check the status of the Postfix mail transport agent service is `systemctl status postfix.service`. This command will display information about the current state of the service, including whether it is running or stopped, any errors or warnings, and the time it was last started or stopped. Note that this command requires administrative privileges (sudo) to run.

## `sudo systemctl stop/start postfix.service`

The `sudo systemctl stop postfix.service` command is used to stop the Postfix mail transport agent service. Note that this command requires administrative privileges (sudo) to run.

# Running MariaDB In a Container

![Screenshot 2023-06-03 at 5.10.28 PM.png](4_Linux%20Administration%20and%20Operation%20in%20the%20Cloud%20da5dbce8b77e4cd4b4e3f5ab73132aff/Screenshot_2023-06-03_at_5.10.28_PM.png)

`sudo yum install docker`

`sudo usermod -a -G docker ec2-user`
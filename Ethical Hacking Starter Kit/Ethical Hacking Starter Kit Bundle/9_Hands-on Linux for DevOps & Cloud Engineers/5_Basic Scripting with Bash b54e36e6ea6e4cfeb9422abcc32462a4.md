# 5_Basic Scripting with Bash

# Learning Bash Fundamental

# Automated  Backup Bash

![Screenshot 2023-06-04 at 11.45.44 AM.png](5_Basic%20Scripting%20with%20Bash%20b54e36e6ea6e4cfeb9422abcc32462a4/Screenshot_2023-06-04_at_11.45.44_AM.png)

```bash
#!/bin/bash

# Check for the directory argument passed in
backup_dir=""
if [ -z $1 ]
then
        # set the directory to engineering if nothing was passed in
        backup_dir="/usr/local/engineering"
else
        backup_dir=$1
fi

# check the directory passed in exists
if [ ! -d $backup_dir ]
then
        echo "The $backup_dir directory does not exist. Backup halted"
        exit 1
fi

# archive name
backup_file_name=/tmp/engineering_$(date +%Y-%m-%d_%H%M%S).tar.gz

# get a count of the files in the directory to be backedup
function files_to_be_backed_up {
        find $backup_dir -type f | wc -l
}

# create the backup archive
echo "Backing up $(files_to_be_backed_up) files"
# send any errors to the backup.log file
tar -czf $backup_file_name $backup_dir 2> /tmp/backup.log

# check for backup archive
if [ -f $backup_file_name ]
then
        echo "Backup succeeded!"
else
        echo "Backup failed!"
fi
```

The code is a Bash script for automated backups of a specified directory. It checks for a directory argument passed in, and if none is given, sets the backup directory to "/usr/local/engineering". If the specified directory does not exist, the script halts and prints an error message. The script then creates a backup archive of the directory specified, with the archive name including the current date and time. The script uses the `find` command to count the number of files in the directory to be backed up, and prints the count. Any errors that occur during the backup process are sent to the "backup.log" file. Finally, the script checks for the existence of the backup archive and prints either a success or failure message.

# Display System Information from Bash

![Screenshot 2023-06-04 at 11.57.16 AM.png](5_Basic%20Scripting%20with%20Bash%20b54e36e6ea6e4cfeb9422abcc32462a4/Screenshot_2023-06-04_at_11.57.16_AM.png)

`**curl -s <http://169.254.169.254/latest/meta-data>**` is a command to retrieve system metadata from a cloud computing instance. This command is often used in cloud environments to retrieve metadata about the instance, such as its instance ID, security group, and IP address. The `-s` flag is used to make the command "silent", meaning it will not display any progress or error messages.

```bash
#!/bin/bash

# host
user=$(whoami)
active_user_count=$(users | wc -w)
hostname=$(uname -n)
disk_used=$(df -Ph | grep xvda1 | awk '{print $4}' | tr -d '\n')
release=$(cat /etc/system-release)

# AWS IMDSv1
instance_id=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
ami_id=$(curl -s http://169.254.169.254/latest/meta-data/ami-id)

# system metrics
memory1=$(cat /proc/meminfo | grep MemAvailable | awk '{print $2}')
memory2=$(cat /proc/meminfo | grep MemTotal | awk '{print $2}')
swap_in_use=$(free | tail -n 1 | awk '{print $3}')
all_processes=$(ps -Afl | wc -l)

# time of day
hour=$(date +"%H")
if [ $hour -lt 12  -a $hour -ge 0 ]
then
        time="morning"
elif [ $hour -lt 17 -a $hour -ge 12 ]
then
        time="afternoon"
else
        time="evening"
fi

#System uptime
uptime=$(cat /proc/uptime | cut -f1 -d.)
up_days=$((uptime/60/60/24))
up_hours=$((uptime/60/60%24))
up_mins=$((uptime/60%60))
up_secs=$((uptime%60))

#System load
load1=$(cat /proc/loadavg | awk {'print $1'})
load5=$(cat /proc/loadavg | awk {'print $2'})
load15=$(cat /proc/loadavg | awk {'print $3'})

echo "

░█▀█░█░█░█▀▀░░░█░░░█▀█░█▀▄
░█▀█░█▄█░▀▀█░░░█░░░█▀█░█▀▄
░▀░▀░▀░▀░▀▀▀░░░▀▀▀░▀░▀░▀▀░

Good $time $user"

#!/bin/bash

# host
user=$(whoami)
active_user_count=$(users | wc -w)
hostname=$(uname -n)
disk_used=$(df -Ph | grep xvda1 | awk '{print $4}' | tr -d '\n')
release=$(cat /etc/system-release)

# AWS IMDSv1
instance_id=$(curl -s http://169.254.169.254/latest/meta-data/instance-id)
ami_id=$(curl -s http://169.254.169.254/latest/meta-data/ami-id)

# system metrics
memory1=$(cat /proc/meminfo | grep MemAvailable | awk '{print $2}')
memory2=$(cat /proc/meminfo | grep MemTotal | awk '{print $2}')
swap_in_use=$(free | tail -n 1 | awk '{print $3}')
all_processes=$(ps -Afl | wc -l)

# time of day
hour=$(date +"%H")
if [ $hour -lt 12  -a $hour -ge 0 ]
then
        time="morning"
elif [ $hour -lt 17 -a $hour -ge 12 ]
then
        time="afternoon"
else
        time="evening"
fi

#System uptime
uptime=$(cat /proc/uptime | cut -f1 -d.)
up_days=$((uptime/60/60/24))
up_hours=$((uptime/60/60%24))
up_mins=$((uptime/60%60))
up_secs=$((uptime%60))

#System load
load1=$(cat /proc/loadavg | awk {'print $1'})
load5=$(cat /proc/loadavg | awk {'print $2'})
load15=$(cat /proc/loadavg | awk {'print $3'})

echo "

░█▀█░█░█░█▀▀░░░█░░░█▀█░█▀▄
░█▀█░█▄█░▀▀█░░░█░░░█▀█░█▀▄
░▀░▀░▀░▀░▀▀▀░░░▀▀▀░▀░▀░▀▀░

Good $time $user"
```

The document contains two Bash scripts. The first script is for automated backups of a specified directory. It checks for a directory argument passed in, and if none is given, sets the backup directory to "/usr/local/engineering". If the specified directory does not exist, the script halts and prints an error message. The script then creates a backup archive of the directory specified, with the archive name including the current date and time. The script uses the `find` command to count the number of files in the directory to be backed up, and prints the count. Any errors that occur during the backup process are sent to the "backup.log" file. Finally, the script checks for the existence of the backup archive and prints either a success or failure message.

The second script displays system information from Bash. The script retrieves system metadata from a cloud computing instance using the `curl` command. Specifically, it retrieves metadata about the instance, such as its instance ID, security group, and IP address. The script then collects various system metrics, including memory usage, swap usage, and the number of running processes. It also calculates system uptime and system load. Finally, the script prints a message with the user's name and the time of day.
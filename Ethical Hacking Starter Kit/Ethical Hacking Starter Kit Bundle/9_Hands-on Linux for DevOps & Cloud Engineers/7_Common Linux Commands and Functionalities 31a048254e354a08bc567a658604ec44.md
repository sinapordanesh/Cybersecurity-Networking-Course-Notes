# 7_Common Linux Commands and Functionalities

# Common Linux Commands

![Screenshot 2023-06-04 at 7.54.30 PM.png](7_Common%20Linux%20Commands%20and%20Functionalities%2031a048254e354a08bc567a658604ec44/Screenshot_2023-06-04_at_7.54.30_PM.png)

![Screenshot 2023-06-04 at 7.55.45 PM.png](7_Common%20Linux%20Commands%20and%20Functionalities%2031a048254e354a08bc567a658604ec44/Screenshot_2023-06-04_at_7.55.45_PM.png)

Here are some common Linux commands and their functionalities:

- **ls**: Lists the files and directories in the current directory
- **cd**: Changes the current directory
- **mv**: Moves a file or directory from one location to another
- **Ctrl+r**: Searches through your command history
- **rm**: Deletes a file or directory
- **find**: Searches for files and directories that meet certain criteria
- **grep**: Searches for a specific string of text in a file or files
- **cat**: Displays the contents of a file
- **tail**: Displays the last few lines of a file
- **less**: Displays a file one page at a time, allowing you to scroll through it

Note that some of these commands can be destructive if used incorrectly, so be careful when using them.

- `ls`
    - `ls -lh`: Lists the files and directories in the current directory with human-readable file sizes and permissions.
    - `ls --help`: Displays a list of available options for the `ls` command.
- `cp`
    - `cp -r`: Copies a directory and its contents to a new location
    - `cp -v`: Verbose output, displaying the names of the files as they are copied
    - `cp -p`: Preserves the permissions and timestamps of the original file or directory
    - `cp -i`: Prompts the user before overwriting an existing file
- `cat -n`: Displays the contents of a file with line numbers.
- `mv -b`: Creates a backup of the original file before moving it to a new location.
- `rm -rf`: Deletes a file or directory and its contents without prompting for confirmation.
- `find . -type f -name -size +10M`: Searches for files larger than 10 megabytes in the current directory and its subdirectories.
- `grep “session” /var/log/secure`: Searches for the string "session" in the `/var/log/secure` file.
- `grep -ri "test_pam” /etc/pam.d`: Searches for the string "test_pam" in all files within the `/etc/pam.d` directory and its subdirectories, with case-insensitive matching.
- `sudo tail -f /var/log/secure`: Displays the last few lines of the `/var/log/secure` file and continues to display any new lines that are added to the end of the file.
- `sudo tail -n 1 /var/log/secure`: Displays only the last line of the `/var/log/secure` file.
- `less cloud/README.md`: Displays the contents of the `README.md` file in the `cloud` directory, allowing you to scroll through it one page at a time.

# Common AWS CLI Commands

![Screenshot 2023-06-04 at 8.08.19 PM.png](7_Common%20Linux%20Commands%20and%20Functionalities%2031a048254e354a08bc567a658604ec44/Screenshot_2023-06-04_at_8.08.19_PM.png)

![Screenshot 2023-06-04 at 8.08.29 PM.png](7_Common%20Linux%20Commands%20and%20Functionalities%2031a048254e354a08bc567a658604ec44/Screenshot_2023-06-04_at_8.08.29_PM.png)

Here are explanations of the AWS CLI commands:

- `aws ec2 describe-instances`: Returns information about one or more instances in an Amazon EC2 instance.
- `aws ec2 run-instances`: Launches one or more Amazon EC2 instances.
- `aws describe-vpcs`: Returns information about one or more virtual private clouds (VPCs).
- `aws describe-security-groups`: Returns information about one or more security groups.
- `aws iam list-users`: Lists the IAM users that have the specified path prefix.
- `aws iam create-user`: Creates a new IAM user for your AWS account.
- `aws iam delete-user`: Deletes the specified IAM user.
- `aws s3api ls`: Lists all of the S3 buckets in your account.
- `aws s3api create-bucket`: Creates an Amazon S3 bucket in the specified region.
- `aws s3api put-object`: Adds an object to an S3 bucket.
- `aws s3api delete-bucket`: Deletes the specified S3 bucket. Note that the bucket must be empty before it can be deleted.
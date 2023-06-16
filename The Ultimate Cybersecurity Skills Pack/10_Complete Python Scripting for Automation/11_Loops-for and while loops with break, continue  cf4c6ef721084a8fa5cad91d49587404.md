# 11_Loops-for and while loops with break, continue and pass

# Practice: Read a Path and Check
If Given Path is a File or a
Directory

![Screenshot 2023-06-15 at 11.11.03 AM.png](11_Loops-for%20and%20while%20loops%20with%20break,%20continue%20%20cf4c6ef721084a8fa5cad91d49587404/Screenshot_2023-06-15_at_11.11.03_AM.png)

```python
import os
path=input("Enter your path: ")
if os.path.exists(path):
	print(f"Given path : {path}is a valid path")
	if os.path.isfile(path):
		print("and it is a file path")
	else:
		print("and it is a directory path")
else:
		print(ƒ"Given path : {path} is not existing on this host") 

```

This Python code prompts the user to enter a file or directory path. It then uses the `os.path.exists()` function to check if the path exists on the host. If the path exists, it prints a message indicating that it is a valid path. The code then uses the `os.path.isfile()` function to determine if the given path is a file or directory, and prints a message accordingly. If the path does not exist, the code prints a message indicating that the path is not existing on this host.

The output is expected to be inserted in place of

# Introduction to Loops with an Example

![Screenshot 2023-06-15 at 11.16.54 AM.png](11_Loops-for%20and%20while%20loops%20with%20break,%20continue%20%20cf4c6ef721084a8fa5cad91d49587404/Screenshot_2023-06-15_at_11.16.54_AM.png)

```python
list_of_files_dir=os.listdir(path)
print("all files and dirs: ",list_of_files_dir)
for each_file_or_dir in list_of_files_dir:
	f_d_p=os.path.join(path, each_file_or_dir)
	if os.path.isfile(f_d_p):
		print(ƒ'{f_d_p} is a file')
	else:
			print(ƒ'{f_d_p} is a directory')
```

# Loops | Working with For Loops

![Screenshot 2023-06-15 at 11.31.27 AM.png](11_Loops-for%20and%20while%20loops%20with%20break,%20continue%20%20cf4c6ef721084a8fa5cad91d49587404/Screenshot_2023-06-15_at_11.31.27_AM.png)

## Why Loops:

All programming languages need a way to execute block of code many times, this is possible with loops.

- Python has two types of loops:
    - for loop
    - while loop

## for loop:

The for loop in Python is used to iterate over a sequence (list, tuple, string) or other iterable objects.

## while loop:

while loop is used to execute a block of statements repeatedly until a given a condition is satisfied.

# Simple Practice with For Loop

![Screenshot 2023-06-15 at 11.34.26 AM.png](11_Loops-for%20and%20while%20loops%20with%20break,%20continue%20%20cf4c6ef721084a8fa5cad91d49587404/Screenshot_2023-06-15_at_11.34.26_AM.png)

```python
usr_str=input("Enter your string: ")
index = 0
for each_char in usr_str:
	print (f'{each_char} --›{index}')
	index += 1
```

## Find All Files in a Directory with Required Extension.py/.sh/.log/.txt etc

```python
import os

req_path = input("Enter your directory path: ")
if os.path.isfile(req_path):
    print(f"The given path {req_path} is a file. Please pass only directory path")
else:
    all_f_ds = os.listdir(req_path)
    if len(all_f_ds) == 0:
        print(f"The given path {req_path} is an empty path")
    else:
        req_ex = input("Enter the required files extension .py/.sh/.log/.txt: ")
        req_files = []
        for each_f in all_f_ds:
            if each_f.endswith(req_ex):
                req_files.append(each_f)
        if len(req_files) == 0:
            print(f"There are no {req_ex} files in the location of {req_path}")
        else:
            print(f"There are {len(req_files)} files in the location of {req_path} with an extension of {req_ex}")
            print(f"so the files are: {req_files}")

```
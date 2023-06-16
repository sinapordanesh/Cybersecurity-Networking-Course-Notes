# 10_OS Module

# Introduction to OS Module and Basic Operations

![Screenshot 2023-06-13 at 2.13.41 PM.png](10_OS%20Module%20f59d339c23344b858d5e5a794f7b56eb/Screenshot_2023-06-13_at_2.13.41_PM.png)

- The `os.sep` module in Python is used to specify the path separator character used by the operating system. This module can be useful when working with file paths and file system operations.
    
    For example, on Unix-based systems, `os.sep` returns `/` as the path separator, while on Windows, it returns `\\`.
    
    Here is an example usage:
    
    ```python
    import os
    
    file_path = "/path/to/file"
    filename = "myfile.txt"
    
    full_path = os.sep.join([file_path, filename])
    
    print(full_path)
    ```
    
    This would output `/path/to/file/myfile.txt` on Unix-based systems, and `\\\\path\\\\to\\\\file\\\\myfile.txt` on Windows.
    
- The `os.getcwd()` method in Python returns the current working directory as a string. This can be useful when working with file paths and file system operations.
    
    Here is an example usage:
    
    ```python
    import os
    current_directory = os.getcwd()
    print(current_directory)
    ```
    
    This would output the current working directory as a string.
    
- The `os.chdir(directory)` method in Python is used to **change** the **current** working directory **to** the **specified** directory. This can be useful when working with file paths and file system operations.
    
    Here is an example usage:
    
    ```python
    import os
    os.chdir('/path/to/directory')
    ```
    
    This would change the current working directory to `/path/to/directory`.
    
- `os.listdir(path)` lists all files and directories in the specified path.
- `os.makedirs(path)` recursively creates directories in the specified path.
- `os.rmdir(path)` removes an empty directory in the specified path.
- The `os.makedirs(path)` method in Python is used to **recursively** create directories in the specified path. Here is an example usage:
    
    ```python
    import os
    
    # Creates a directory named 'parent'
    os.makedirs('/path/to/parent/directory')
    
    # Creates a directory named 'child' inside the 'parent' directory
    os.makedirs('/path/to/parent/directory/child')
    ```
    
    This code will create a directory named `parent` at the specified path, and then a directory named `child` inside the `parent` directory.
    
    It is important to note that if the specified path already exists, `os.makedirs()` will not raise an error and will not overwrite the existing directory.
    
- `os.rename(src, dst)` is used to rename a file or directory. Here is an example usage:
    
    ```
    import os
    
    os.rename('/path/to/old/file.txt', '/path/to/new/file.txt')
    
    os.rename('/path/to/old/directory', '/path/to/new/directory')
    
    ```
    
- The `os.environ()` method in Python returns a dictionary containing the environment variables of the current process. Here is an example usage:
    
    ```python
    import os
    env_variables = os.environ
    print(env_variables)
    ```
    
- The `os.getuid()` method in Python returns the current process's user ID. Here is an example usage:
    
    ```python
    import os
    uid = os.getuid()
    print(uid)
    
    ```
    
- The `os.getpid()` method in Python returns the current process's process ID. Here is an example usage:
    
    ```python
    import os
    pid = os.getpid()
    print(pid)
    ```
    

# os.path Module

![Screenshot 2023-06-13 at 2.27.18 PM.png](10_OS%20Module%20f59d339c23344b858d5e5a794f7b56eb/Screenshot_2023-06-13_at_2.27.18_PM.png)

The `os.path` module in Python provides a way to work with file paths and file system operations in a platform-agnostic way. Some of the functions provided by this module include:

- `os.path.join(path, *paths)` joins one or more path components intelligently. This can be useful when working with file paths and file system operations. Here is an example usage:
    
    ```python
    import os
    
    path1 = '/path/to'
    path2 = 'file.txt'
    
    full_path = os.path.join(path1, path2)
    
    print(full_path)
    ```
    
    This would output `/path/to/file.txt` on both Unix-based systems and Windows.
    
- `os.path.exists(path)` returns `True` if the specified path **exists**, and `False` otherwise.
- `os.path.isfile(path)` returns `True` if the specified path is a file, and `False` otherwise.
- `os.path.isdir(path)` returns `True` if the specified path is a directory, and `False` otherwise.
- `os.path.islink(path)` returns `True` if the specified path is a symbolic link, and `False` otherwise.
- `os.path.getsize(path)` returns the size of the file in bytes, or raises an error if the specified path is a directory.
- `os.path.basename(path)` returns the base name of the specified path, which is the final component of the path, without any leading directory separators.
- `os.path.dirname(path)` returns the directory component of the specified path, without the final component.
- `os.path.split(path)` splits the specified path into its directory and file components, and returns them as a tuple.
- `os.path.splitext(path)` splits the specified path into its base name and extension components, and returns them as a tuple.
- `os.path.normpath(path)` normalizes the specified path, eliminating double slashes and resolving any symbolic links.
- `os.path.abspath(path)` returns the absolute path of the specified path, resolving any symbolic links and relative path components.
- `os.path.relpath(path, start)` returns a relative path from the `start` path to the `path` path.

These functions can be used to manipulate and work with file paths and file system operations in a platform-agnostic way.

# `os.system()` Function from OS Module

The `os.system()` function in Python is used to execute a command in the shell or command prompt. Here is an example usage:

```python
import os
os.system('ls')
```

This would execute the `ls` command in the shell or command prompt and return the output. The `os.system()` function can be used to execute any command that can be run in the shell or command prompt.

It is important to note that the `os.system()` function is deprecated and has been replaced by the `subprocess` module in Python 3.5 and later. The `subprocess` module provides more powerful and secure ways to execute commands in the shell or command prompt.

# Practice Script on Platform and OS Module

![Screenshot 2023-06-13 at 2.39.32 PM.png](10_OS%20Module%20f59d339c23344b858d5e5a794f7b56eb/Screenshot_2023-06-13_at_2.39.32_PM.png)

```python
import os
import platform
if platform.system()=="windows":
else:
os.system("cls")
os.system("clear")
```

The code above is a Python script that clears the terminal screen. It uses the `os` and `platform` modules to determine the operating system being used and then executes the appropriate command to clear the terminal. If the operating system is Windows, it uses the `cls` command to clear the screen. Otherwise, it uses the `clear` command. The script can be useful when working on the command line or in a terminal environment to clear the screen and make it easier to read output.

# `os.walk(path)` Command

![Screenshot 2023-06-13 at 2.47.21 PM.png](10_OS%20Module%20f59d339c23344b858d5e5a794f7b56eb/Screenshot_2023-06-13_at_2.47.21_PM.png)

The `os.walk(path)` command in Python generates the file names in a directory tree by walking the tree either top-down or bottom-up. For **each directory** in the tree, it yields a **3-tuple `(dirpath, dirnames, filenames)`**. Here is an example usage:

```python
import os

for dirpath, dirnames, filenames in os.walk('/path/to/directory'):
    print(f'Found directory: {dirpath}')
    for file_name in filenames:
        print(f'\\t{file_name}')
```

This code will recursively traverse the directory tree starting at `/path/to/directory`, and for each directory it finds, it will print the directory name and the names of all files in that directory.

# Best Practice with `os.walk()` for Real-time

![Screenshot 2023-06-13 at 3.06.56 PM.png](10_OS%20Module%20f59d339c23344b858d5e5a794f7b56eb/Screenshot_2023-06-13_at_3.06.56_PM.png)

## Example 1 - (linux version)

```python
import os
req_file=input("Enter your file name to search: ")
for r,d,f in os.walk ("/"):
	for each file in f:
		if each_file==req_file:
			print (os.path.join(r, each_file))
```

This code uses the `os` module to search for a specified file name in the file system. The user is prompted to enter the name of the file they are searching for. Then, the `os.walk()` function is used to traverse the file system tree, starting at the root directory ("/"). For each directory in the tree, it searches for the specified file name in the list of files in that directory. If the file is found, it prints the full path to the file.

The code is incomplete as it lacks the condition for the if statement. A possible condition would be `if each_file == req_file:`.

## Example 2 - (windows/linux)

```python
import os
import string
import platform

req_file=input("Enter your file name to search: ")

if platform.system()=="Windows":
	pd_names=string.ascii_uppercase
	vd_names=[]
	for each_drive in pd_names:
		if os.path.exists(each_drive+":\\"):
			#print(each_drive)
			vd_names.append(each_drive+":\\")
	print(vd_names)
	for each_drive in vd_names:
		for r,d,f in os.walk(each_drive):
			for each_f in f:
				if each_f==req_file:
					print(os.path.join(r,each_f))
else:
	for r,d,f in os.walk("/"):
		for each_file in f:
			if each_file == req_file:
				print (os.path.join(r,each_file))
```

This Notion document provides an introduction to the `os` module in Python and its basic operations. It covers the `os` and `os.path` modules, the `os.system()` function, and the `os.walk(path)` command. The document includes examples of how to use these functions to work with file paths and file system operations, execute commands in the shell or command prompt, and generate file names in a directory tree. Finally, the document includes two examples of using `os.walk()` to search for a file in the file system, one for Windows and one for Linux.
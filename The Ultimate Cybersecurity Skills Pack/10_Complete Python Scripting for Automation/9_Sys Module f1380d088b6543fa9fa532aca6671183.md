# 9_Sys Module

# Introduction to sys Module

![Screenshot 2023-06-13 at 1.51.57 PM.png](9_Sys%20Module%20f1380d088b6543fa9fa532aca6671183/Screenshot_2023-06-13_at_1.51.57_PM.png)

The code `import sys` is a Python statement that allows us to use the `sys` module in our Python code. The `sys` module provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter.

`sys.version_info` is a tuple containing the version number of the Python interpreter. It can be used to check which version of Python is being used, and to write code that is compatible with different versions of Python.

The `sys.modules` attribute is a dictionary that maps module names to modules that have already been loaded into memory. It can be useful for inspecting the modules that are currently available in your Python environment.

The `sys.path` attribute is a list of strings that specifies the search path for modules. When a module is imported, Python looks for it in the directories listed in `sys.path`, in the order in which they are listed. You can add directories to the search path by appending them to the `sys.path` list.

Example usage:

```python
import sys
print(sys.path)
```

This will print out a list of directories where Python looks for modules.

`sys.exit` is a function in the `sys` module that allows you to exit a Python program. When called, it raises the `SystemExit` exception, which can be caught and handled in a `try`/`except` block.

Example usage:

```python
import sys

try:
    # some code here
    sys.exit(0) # exit with status code 0
except SystemExit as e:
    print(f"Program exited with status code {e.code}")
```

# sys.argv | Working with Command Line Arguments with an Example

![Screenshot 2023-06-13 at 1.58.33 PM.png](9_Sys%20Module%20f1380d088b6543fa9fa532aca6671183/Screenshot_2023-06-13_at_1.58.33_PM.png)

`sys.argv` is a list in Python that contains the command-line arguments passed to the script. It is used to handle command-line arguments in Python scripts, including complex parsing.

Example:

```python
import sys

if len(sys.argv) != 3:
	print("Usage:")
	print(ƒ'{sys.argv[0]} <your_req_string> <lower|upper|title>'| )
	sys.exit()

usr_str=sys.argv[1]
usr_action=sys.argv[2]

if usr_action=="lower":
	print(usr_str.lower())
elif usr_action=="upper":
	print(usr_str.upper())
elif usr_action ="title":
	print(usr_str.title())
else:
	print("Your option is invalid. Please select valida option from this list: lower/upper/title")
```
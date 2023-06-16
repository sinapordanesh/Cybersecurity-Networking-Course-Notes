# 8_Working with Python Modules

# Platform Modules

![Screenshot 2023-06-13 at 1.21.02 PM.png](8_Working%20with%20Python%20Modules%2021363adc94c94f278b4355755304076d/Screenshot_2023-06-13_at_1.21.02_PM.png)

You can use the `help('modules')` command in the Python terminal to get a list of all available modules in your Python environment.

## How to use

To use the platform module in a Python script, first import it using one of the following syntaxes:

```python
import platform
import platform as pt
from platform import *
from platform import system, platform
```

To list all the functions and variables of the platform module, use the built-in dir() function as follows:

```python
print(dir(platform))
```

To get help on the platform module, use one of the following:

```python
print(help(platform)) # from a script
help(platform) # from the Python command line
```

To print the system type using the `platform` module in Python, use the following code:

```python
import platform
print(platform.system())
```

To print the version of Python you are currently using, you can use the `python_version()` function from the `platform` module in Python. Here is an example:

```python
import platform
print(platform.python_version())
```

To print the system/OS information using the `platform` module in Python, you can use the `uname()` function. Here is an example:

```python
import platform
print(platform.uname())
```

# Getpass Module

![Screenshot 2023-06-13 at 1.28.18 PM.png](8_Working%20with%20Python%20Modules%2021363adc94c94f278b4355755304076d/Screenshot_2023-06-13_at_1.28.18_PM.png)

The `getpass` module provides a simple way to prompt the user for a password or other secret information without echoing what is typed to the console. To use this module, import it as follows:

```python
import getpass
```

To prompt the user for a password, use the `getpass()` function.

The `getuser` module is used to get the name of the logged-in user. To use this module, import it as follows:

```python
import getpass
```

Then, to get the name of the current user, use the `getuser()` function.
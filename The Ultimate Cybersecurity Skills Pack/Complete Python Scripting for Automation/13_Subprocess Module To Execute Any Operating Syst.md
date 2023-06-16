# 13_Subprocess Module: To Execute Any Operating System Commands with Python

# Introduction to Subprocess Module

## Python Subprocess Module

The `subprocess` module is a Python module that enables users to execute any operating system commands from within their Python code. It allows users to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

This module is particularly useful for running system commands and scripts from within Python scripts. It also allows users to retrieve the output of those commands and scripts, and use them for further processing within their Python code.

![Screenshot 2023-06-15 at 12.22.47 PM.png](13_Subprocess%20Module%20To%20Execute%20Any%20Operating%20Syst%208338b4fd80e846c3a1cb0d2a90a3d5e4/Screenshot_2023-06-15_at_12.22.47_PM.png)

![Screenshot 2023-06-15 at 12.23.14 PM.png](13_Subprocess%20Module%20To%20Execute%20Any%20Operating%20Syst%208338b4fd80e846c3a1cb0d2a90a3d5e4/Screenshot_2023-06-15_at_12.23.14_PM.png)

```python
import subprocess

cmd="ls -lrt"
sp=subprocess.Popen(cmd, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)
rc=sp.wait()
out, err=sp.communicate()
print(f'The return code: {rc}')
print(f'The output: \\n{out.splitlines()}')
print(f'The error: \\n{err.splitlines()}')

#cmd="ls -lrt".split()
#cmd=['ls','-1rt']
#cmd='echo $HOME'.split()
cmd=['echo', '$HOME']
sp=subprocess.Popen(cmd, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)
rc=sp.wait()
out, err=sp.communicate()
print(f'The return code: {rc}')
print(f'The output: \\n{out.splitlines()}')
print(f'The error: \\n{err.splitlines()}')

```

The code above demonstrates the use of the `subprocess` module to execute operating system commands from within Python code.

The first example demonstrates the use of `subprocess.Popen()` to execute the command `ls -lrt`. The `Popen()` function takes several arguments, including the command to be executed and the desired output streams. In this case, the `stdout` and `stderr` streams are redirected to `PIPE`, and `universal_newlines=True` is used to ensure that the output is returned as a string rather than bytes. The `wait()` function is used to wait for the process to complete, and `communicate()` is used to retrieve the output and error streams.

The second example demonstrates the use of `Popen()` to execute the command `echo $HOME`. This example also shows how to pass a command as a list of arguments rather than a single string, which can be useful for commands with arguments that contain spaces or other special characters.

# Practice - 1 with Subprocess Module

```python
import subprocess

cmd=["bash","--version"]
sp=subprocess.Popen(cmd, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)
rc=sp.wait()
o,e=sp.communicate()
if rc==0:
    for each_line in o.splitlines():
        if "version" in each_line and "release" in each_line:
            print(each_line.split()[3].split('(')[0])
else:
    print("Command was failed and error is: ",e)

```

The code above uses the `subprocess` module to execute the command `bash --version`. The `Popen()` function is called with the command and desired output streams as arguments. The `wait()` function is called to wait for the process to complete, and `communicate()` is used to retrieve the output and error streams. If the return code is 0, the output is searched for the version and release information, which is printed to the console. If the return code is not 0, the error message is printed to the console.

# Practice - 2: Platform Independent Script to Find the Java Version

```python
import subprocess

cmd = "java -version"
sp = subprocess.Popen(cmd, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE, universal_newlines=True)
rc = sp.wait()
o, e = sp.communicate()

if rc == 0:
    if bool(o) == True:
        print(o)
    else:
        if bool(o) == False and bool(e) == True:
            print(e.splitlines()[0].split()[2].strip("\\""))
            print(e)

```

The code above uses the `subprocess` module to execute the command `java -version`.
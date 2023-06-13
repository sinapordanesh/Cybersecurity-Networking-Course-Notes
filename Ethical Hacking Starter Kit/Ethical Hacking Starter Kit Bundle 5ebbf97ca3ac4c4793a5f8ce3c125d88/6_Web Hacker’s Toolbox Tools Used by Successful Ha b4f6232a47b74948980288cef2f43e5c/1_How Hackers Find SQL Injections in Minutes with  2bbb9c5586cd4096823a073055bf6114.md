# 1_How Hackers Find SQL Injections in Minutes with Sqlmap

# Introduction

- SQL injection
- Manual vs. automated testing
- Automated SQL injection detection and exploitation
- Tool?
- Sqlmap

## Table of Contents

- The Basics of Sq|map
- Dumping Database Table Entries
- From SQL Injection to Remote Code Execution
- More Advanced Testing with Sq|map
- Bypassing Web Application Firewalls

# The Basics of Sqlmap

## `sqlmap -u "{url}" --banner`

- `sqlmap -u "{url}" --banner` retrieves the **DBMS banner information** of the target web application.
- The banner information includes the **name, version, and other details** of the DBMS.
- The command takes a **URL of the target page where the SQL injection vulnerability exists**.
- Sqlmap sends specific payloads to the target URL to **determine the type of DBMS used**.
- Once the DBMS is identified, sqlmap retrieves the banner information by **sending a specially crafted HTTP request**.
- The banner information can be useful to **launch targeted attacks against known vulnerabilities** of that version.
- It is also helpful to check if the target web application is **vulnerable to any known SQL injection attack vectors**.

## `sq|map -u "{url}" --banner —cookie="{cookie set}"`

`sqlmap -u "{url}" --banner --cookie="{cookie set}"` is similar to `sqlmap -u "{url}" --banner`, but includes an additional parameter to specify a cookie value for the HTTP request. This can be useful in cases where the web application requires authentication, and the SQL injection vulnerability only exists after logging in. By setting the cookie value, sqlmap can simulate a logged-in user and test for SQL injection vulnerabilities in authenticated areas of the application.

The `--cookie` parameter must be followed by the name-value pair of the cookie, separated by an equals sign. For example, if the cookie name is `session` and the value is `abc123`, the parameter would be `--cookie="session=abc123"`.

# Dumping Database Table Entries - Overview

- Fetching the database banner is just a proof of concept
- SQL injection - let's dump database table entries!

## `sqlmap -u "{url}" --dump`

`sqlmap -u "{url}" --dump` is used to dump the contents of a database table. This command should only be used on systems where you have explicit permission to do so, as it can result in sensitive information being exposed.

To use the command, replace `{url}` with the URL of the target page where the SQL injection vulnerability exists. Sqlmap will automatically detect the type of database management system (DBMS) used by the target web application, and dump the contents of the first table in the database by default.

If you want to dump a **specific table**, you can use the `--table` parameter followed by the name of the table. For example, to dump the contents of a table called `users`, you would use the command `sqlmap -u "{url}" --dump --table users`.

# Form SQL Injection to Remote Code Execution - Overview

- SQL injection - install a backdoor - remote code execution

## `sqlmap -u "{url}" -os-shell`

- `sqlmap -u "{url}" -os-shell` allows you to execute arbitrary commands on the targeted system by installing a backdoor.
- This command should only be used on systems where you have explicit permission to do so, as it can result in unauthorized access to the system.
- Replace `{url}` with the URL of the target page where the SQL injection vulnerability exists.
- Once sqlmap has identified the type of DBMS used by the target web application, it will attempt to install a backdoor on the system.
- After installation, sqlmap will provide you with an interactive shell that allows you to execute arbitrary commands on the targeted system.
- Simply type the command you want to execute at the prompt and press Enter.
- For example, to execute the command `whoami`, you would type `whoami` at the prompt and press Enter.
- The `os-shell` command is only available for certain DBMS types, such as MySQL and PostgreSQL.
- If the command is not available for the target DBMS, you will receive an error message.

# More Advanced Testing with Sqlmap

## `sqlmap -u "{url}" —data="{data}” —banner`

- The `sqlmap -u "{url}" —data="{data}” —banner` command is used to retrieve the DBMS banner information, similar to `sqlmap -u "{url}" --banner`.
- **However**, this command includes an additional parameter to specify the POST data to be sent in the HTTP request.
- This can be useful in cases where the SQL injection vulnerability exists in a POST request, rather than a GET request.
- The `—data` parameter must be followed by the POST data, as a string in the format `name1=value1&name2=value2&name3=value3`.
- For example, if the POST data includes two parameters, `username` and `password`, the parameter would be `—data="username=admin&password=password123"`.

## `sqlmap -u "{url}" —data="{data}” --rist={#risk} --level={#level} —banner`

- `sqlmap -u "{url}" —data="{data}” --risk={#risk} --level={#level} —banner` retrieves DBMS banner information with additional parameters to control risk and testing levels.
- `-risk` specifies the level of risk for testing SQL injection vulnerabilities (1, 2, or 3). The default is 1.
- `-level` specifies the depth of testing (1, 2, or 3). The default is 1.
- Use `—data` to provide POST data in `name1=value1&name2=value2&name3=value3` format.
- Example: `sqlmap -u "{url}" —data="{data}” --risk=2 --level=2 —banner`.

# Bypassing Web Application Firewalls

- No injection point detected
- Maybe the attack is blocked by Web Application Firewall (WAF)
- Let's try to bypass the Web Application Firewall with a tamper script (e.g. random case; "SELECT" -> "sELeCt")

## `sqlmap -u "{url}" --risk=3 --level=5 --tamper=randomcase --banner`

This command is using sqlmap to test for SQL injection vulnerabilities in a target web application.

- `u "{url}"` specifies the URL of the target page where the SQL injection vulnerability exists.
- `-risk=3` sets the level of risk for testing SQL injection vulnerabilities to 3, which is the highest risk level.
- `-level=5` specifies the depth of testing to level 5, which is the highest testing level. This means that sqlmap will use more aggressive testing techniques to try to identify vulnerabilities.
- `-tamper=randomcase` is a tamper script that sqlmap will use to try to **bypass a web application firewall**. In this case, the tamper script will randomly change the case of SQL keywords, such as "SELECT" becoming "sELeCt". This can help to bypass certain types of web application firewalls that are looking for specific SQL keywords.
- `-banner` retrieves the DBMS banner information of the target web application.

# Summary

- **Sqlmap**
- Automated SQL injection detection and exploitation
- Testing GET parameters and fetching the database banner
- Exploitation: dumping database table entries
- Exploitation: from SQL injection to remote code execution
- Testing POST parameters and sending the maximum number of payloads
- Bypassing web application firewalls with a tamper script
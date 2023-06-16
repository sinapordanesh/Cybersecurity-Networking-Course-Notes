# 12_Datetime Module to Work with Dates and Times

# Introduction to Datetime Module

![Screenshot 2023-06-15 at 11.51.46 AM.png](12_Datetime%20Module%20to%20Work%20with%20Dates%20and%20Times%206d7d371acfe547449961d7b421f950b7/Screenshot_2023-06-15_at_11.51.46_AM.png)

The `datetime` module provides the following classes:

- `datetime.date`: Represents a date (year, month, day)
- `datetime.time`: Represents a time (hour, minute, second, microsecond)
- `datetime.datetime`: Represents a date and time (year, month, day, hour, minute, second, microsecond)
- `datetime.timedelta`: Represents a duration or difference between two dates or times
- `datetime.tzinfo`: Abstract base class for dealing with time zones

You can use these classes to work with dates and times in Python.

# Find all the files which are older than x days

```python
import os
import sys
import datetime

req_path=input("Enter your path: ")
age=3

if not os.path.exists(req_path):
    print("Please provide valid path ")
    sys.exit(1)

if os.path.isfile(req_path):
    print("Please provide directory path ")
    sys.exit(2)

today=datetime.datetime.now()
for each_file in os.listdir(req_path):
    each_file_path=os.path.join(req_path, each_file)
    if os.path.isfile(each_file_path):
        file_cre_date=datetime.datetime.fromtimestamp(os.path.getctime(each_file_path))
        dif_days=(today - file_cre_date).days
        if dif_days > age:
            print(each_file_path,dif_days)
```
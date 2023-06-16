# 15_Working with CSV Files

## First of all, what is a CSV?

- CSV --> Comma Separated Values
- It is a simple file format used to store tabular data, such as a spreadsheet/excel or database.
- CV is convenient way to export data to spreadsheets and databases as well as import or use it in other programs.

```python
import csv
req_file="C:\\Users\\Automation\\Desktop\\hi\\new_info.csv"

fo=open(req_file,"r")
content=csv.reader(fo,delimiter="|")
for each in content:
	print(each)

fo.close()
```

## Read Headers and No of Rows

To read the headers and number of rows in a CSV file using Python, you can use the following code:

```python
import csv

req_file="C:\Users\Automation\Desktop\hi\new_info.csv"

with open(req_file,"r") as fo:
    content = csv.reader(fo, delimiter="|")
    headers = next(content)
    rows = [row for row in content]
    print("Headers: ", headers)
    print("Number of Rows: ", len(rows))
```

This code reads in the CSV file located at `req_file` and uses the `csv.reader` function to parse the file. The `next` function is called to get the headers of the CSV file, and then a list comprehension is used to get all the rows. Finally, the number of rows is printed along with the headers.

To create a CSV file using Python, you can use the following code:

```python
import csv

req_file="C:\\Users\\Automation\\Desktop\\hi\\new_info.csv"

with open(req_file,"w",newline="") as fo:
    writer=csv.writer(fo,delimiter="|")
    writer.writerow(["Name","Age","Gender"])
    writer.writerow(["John","32","Male"])
    writer.writerow(["Jane","28","Female"])
```

This code creates a new CSV file located at `req_file` and uses the `csv.writer` function to write rows to the file. The `writerow` function is called to write each row of data to the file, and the `delimiter` argument is set to "|" to specify that the file should use pipes as the delimiter between values.
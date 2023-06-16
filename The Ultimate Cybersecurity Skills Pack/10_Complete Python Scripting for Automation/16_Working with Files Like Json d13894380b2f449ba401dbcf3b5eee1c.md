# 16_Working with Files Like Json

JSON:

- JSON (JavaScript Object Notation) is a popular data format used for representing structured data.
- It's common to transmit and receive data between a server and web application in JSON format.

```python
import json

my_dict = {'Name': 'Narendra', 'skills' :['Python', 'shell', 'yamI', 'AWS']}

req_file = "myinfo.json"

fo = open(req_file, 'w')
json.dump(my_dict, fo, indent=4)

fo.close()

```

The above code is an example of how to write a Python dictionary to a JSON file. The dictionary `my_dict` contains information about a person's name and skills. The file is opened in write mode and the `json.dump()` function is used to write the dictionary to the file. The `indent` argument is set to 4 to make the output more readable. Finally, the file is closed using the `fo.close()` function.
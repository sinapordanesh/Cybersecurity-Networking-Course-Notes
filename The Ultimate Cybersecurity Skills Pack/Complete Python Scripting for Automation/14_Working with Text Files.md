# 14_Working with Text Files

# Reading and Writing to Text Files

# Python Reading and Writing to Text Files

Python has built-in functions and methods to easily read and write to text files.

To read a text file, use the `open()` function to create a file object and then use the `read()` method to get the file contents.

To write to a text file, use the `open()` function with the mode `"w"` for writing and the `write()` method to write to the file.

```python
# Reading a text file
with open("example.txt", "r") as file:
    contents = file.read()

# Writing to a text file
with open("example.txt", "w") as file:
    file.write("Hello, world!")

```

Remember to always close the file object when finished reading or writing using the `close()` method or the `with` statement.

# Copy one File to Another

```python
sfile="C:\\Users\\Automation\\Desktop\\random.txt" 
dfile="C:\\Users\\Automation\\Downloads\\newrandom.txt" 
#sfile=input("Enter your source file: ") #dfile=input("Enter your destination file: ")
sfo=open(sfile)
print(sfo.mode) 
content=sfo.read() 
sfo.close()

dfo=open(dfile, 'w') 
dfo.write(content) 
dfo.close()
```
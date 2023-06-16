# 17_Exception Handling

```python
try:
   a=9
   print(a)
except NameError:
   print("Variable is not defined")
except Exception as e:
   print("Exception occured:", e)
else:
   # executes if the code inside try block does not raise exception
finally:
   # executes no matter what, whether exception was raised or not
   print ("This will execute if there is no exceptions in try block")
   print ("This will executes always")

```
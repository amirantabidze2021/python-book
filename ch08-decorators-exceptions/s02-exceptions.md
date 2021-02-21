# Exceptions

Errors detected during execution are called **exceptions** and are not unconditionally fatal

* It is Pythonic way to use them as much often as possible
* Sometimes you can't predict all possible values and situations
    * No heaps of if else conditions

General form:

```python
try:
    <code> 
except <ExceptionName> as <alias>:
    <code in case of error happened>
else: 
    <code if everything was OK>
finally: 
    <code in any case>
```

We are checking the code only after `try` before `except`.


```python
def divide_ten(num): 
    try: 
        print(10.0 / num )
    except ZeroDivisionError as e: 
        print(f"Oops, invalid - you can't pass 0. Error: {e}") 
    except TypeError:
        print("Wrong type!", type(num))
    except Exception as e:
        print("Unexpected exception:", e)
    else: 
        print("Cool, no exceptions were triggered!") 
    finally: 
        print("We're done with that.")

print("1)")        
divide_ten("2") 
print("2)")
divide_ten(0)
print("3)")
divide_ten(3)
```

    1)
    Wrong type! <class 'str'>
    We're done with that.
    2)
    Oops, invalid - you can't pass 0. Error: float division by zero
    We're done with that.
    3)
    3.3333333333333335
    Cool, no exceptions were triggered!
    We're done with that.


Another working example:

Checking user's input and returning the list item.
Non-ideal solution would be:


```python
l = list(range(10))

def get_item():
    num = input("Enter index: ")
    if not num.isdigit():
        return "Incorrect value"
    if len(l) < int(num):
        return "Out of range"
    return l[int(num)]
```

Better solution:


```python
def get_item():
    num = input("Enter index: ")
    try:
        return l[int(float(num))]
    except IndexError:
        return "Out of range"
    except (TypeError, ValueError):
        return "Incorrect value"
    except Exception as e:
        return f"Unexpected exception: {e.__class__.__name__}({e})"
```

## Custom Exceptions 

```python
class SimpleCustomException(Exception):
    pass

class CustomException(Exception): 
    def __init__(self, value="Some error"): 
        self.parameter = value 
        
    def __str__(self): 
        return self.parameter
```

For raising custom Exception – `raise` used:

* `raise CustomException`

* `raise CustomException()`


```python
# divide.py :
class NegativeException(Exception): 
    def __init__(self, message="Can't work with negative numbers"):
        #logger.error("...")
        self.message = message
    
    def __str__(self):
        return "ERROR: " + self.message

def divide_ten(num):
    if num < 0:
        raise NegativeException
    return 10.0 / num

#========================
# from divide import divide_ten, NegativeException

def main(num):
    try:
        print(
            divide_ten(num)
        )
    except ZeroDivisionError:
        print("Oops, can't div by zero!")
    except NegativeException as e:
        print(e) 

main(0)
main(-6)
main(3)
```

    Oops, can't div by zero!
    ERROR: Can't work with negative numbers
    3.3333333333333335


## Referring to exceptions

Please note that `raise` can also be used to print an error message and then re-raise the exception (allowing a caller to handle the exception as well):


```python
import sys

try:
    f = open('/tmp/1123123.txt')
    s = f.readline()
    i = int(s.strip())
except TypeError:
    print("Wrong type")
except ValueError as e:
    print(f"Could not convert data to an integer: {e}")
except OSError as err: 
    print("OS error: {}".format(err))
    print(err.filename)
except:
    print("Unexpected error:", sys.exc_info())
    raise
```

    OS error: [Errno 2] No such file or directory: '/tmp/1123123.txt'
    /tmp/1123123.txt


## Catching multiple exceptions

* Several except blocks
* Putting several exceptions in a tuple


```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except (IOError, ValueError) as e: 
    print("Data or file error: %s" % e )
```

    Data or file error: [Errno 2] No such file or directory: 'myfile.txt'


## assert

> Testing for poor ones

Debug version of raise with condition:

`assert <test>[, <data>]`

is equivalent to:

```python
if __debug__: 
    if not <test>: 
        raise AssertionError(<data>)
```

`__debug__` is special bool variable (interpreter-level constant (one of very few ones!)) which allways is True unless `python` is called with `-O` (optimization, capital O – not a zero!)

```sh
python –O script.py
```

Examples of `assert`:


```python
assert 1 == 1
assert len(range(5)) == 5
try:
    assert 2 + 2 == "2 + 2", "On paper it works..."
except AssertionError as e:
    print("Cought AssertionError:", e)
```

    Cought AssertionError: On paper it works...
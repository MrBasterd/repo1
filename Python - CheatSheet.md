## Everything Python

---

* CPython is first compiled to bytecode than that code is interpreted

---
```python
dir(<object>) # returns a list of valid attributes for that object
              # is used to find out which names a module defines
              # without arguments it lists the names you have defined currently
help(<help>)  # returns the help documentation of tthe given object 
# If you want the names of built-in functions and variables one can use:
import builtins
dir(buildints)
```

* __in__ and __not in__ check whether a value occurs or does not occur in a squence

* __is__ and __is not__ compare whether two objects are really the same object 

* The __break__ statement breaks out of the innermost enclosing `for` or `while` loop

* The __continue__ statement continues with the next iteration of the loop

* The __pass__ statement does nothing and can be used as a placeholder statement if one is required syntactically

* `isinstance(obj, class)` checks an instance'stype against another

* `ìssubclass(bool, int)` is True

* `print(my_instance.__dict__)` returns the namespace dictionary

---

#### Functions

* A method is a function that 'belongs to' an object

* the first statement of the function body can be a string literal called the __"""docstring"""__ e.g. 

```python
def my_function():
    """Do nothing, but document it.

        No, really, it doesn't do anything.
        """
    pass
```

* When a function is executed a new nymbol table is introduced, which holds the variables of the function. All variable assignments in a function store the value in the local symbol table. 

    1. local symbol table
    1. local symbol table of enclosing functions
    1. global symbol table
    1. table of built-in names

    This is also why global variables can't be directly assigned a value in a function

    * from stackoverflow: 
    > 1. the parameter passed in is actually a reference to an object (but the reference is passed by value) 
    > 2. some data types are mutable, but others aren't
    
    > So:

    > If you pass a mutable object into a method, the method gets a reference to that same object and you can mutate it to your heart's delight, but if you rebind the reference in the method, the outer scope will know nothing about it, and after you're done, the outer reference will still point at the original object.

    > If you pass an immutable object to a method, you still can't rebind the outer reference, and you can't even mutate the object.
    > When you call a function with a parameter, a new reference is created that refers to the object passed in. This is separate from the reference that was used in the function call, so there's no way to update that reference and make it refer to a new object.

    * So if a function is called with a certain parameter a new reference to the object is created, so you can actually change the input object, since you have the same referenced object as in the outside scope, but you can't do anything about the original reference to the object since you're function is working with a new one, which means you cant for instance reassign the original reference to some new object.

    * If you have an immutable object as parameter you can't do shit

* One can set default values in functions e.g. `my_function(age, def_param = None)`, which can but doesn't have to be specified when calling the function. So the the function behaves differrently if the argument is present. All standard arguments first than default ones, otherwise the language doesn't  know whether a default value is set or not.
__Default arguments are evaluated at definition time__

* In a function call, keyword arguments must follow positional arguments. Functions can be called using keyword arguments e.g. `parrot(action='VOOOOOM', voltage=1000000)`. When a final formal parameter of the form `**name` is present, it receives a dictionary containing all keyword arguments except for those corresponding to a formal parameter.

* A Formal parameter is in the functin definition, and an argument is in a function call.

* A formal parameter in the form of `*name` receives a tuple containing the positional arguments beyond the formal parameter list. If one wants to specifiy that a function can be called with an arbitrary number of arguments `*name` is used. `*name` must occure before `**name`.

* If the arguments are already in a list or tuple the `*`-Operator can be used to unpack the arguments.

```python
args = [3, 6]
list(range(*args)) 
[3, 4, 5]  

def parrot(voltage, state='a stiff', action='voom'):
    print("-- This parrot wouldn't", action, end=' ')
    print("if you put", voltage, "volts through it.", end=' ')
    print("E's", state, "!")

d = {"voltage": "four million", "state": "bleedin' demised", "action": "VOOM"}
parrot(**d)
This parrot wouldn't VOOM if you put four million volts through it. E's bleedin' demised !
```

* Small functions can be created with the `lambda`- keyword, which can be used wherever function objects are needed. They are syntactically restricted to a single expression e.g. `lambda a, b: a+b`, which returns the sum of it's two arguments.
---


#### Iterators

* an iterator is an object that represents a stream of data, returns the data one element at a time

* any object that supports iteration is called iterable

```python
string = "1234567890"
for char in string: # for loop uses iterator to return the items
    print(char)
# when there are no more items an error is thrown which the for loop handles
# can also be written as
my_iterator = iter(string)
print(next(my_iterator))
print(next(my_iterator))
```
* a for loop is creating a iterator from the iterable string object

---

#### Lists

* A List is an a ordered and changeable object

```python
#init an empty list
my_list = list()
my_list = []
```

* using the sorted() function returns a new list not altering the original

* It is easy to use lists as a stack with the `append()` and `pop()` functions

* It's also possible to use them as queues, but since inserts or pops from the beginning of a list is slow (`collections.deque()`)

* List comprehension provides a concise way to create lists

```python
squares = list(map(lambda x: x**2, range()))
squares = [x**2 for x in range(10)]
# Both create a list of the numbers 0 to 9 squared
[(x,y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
```
* a list comprehension consists of brackets containing an expression followed by a for clause and that followed by as many for if clauses as one wants

* They can also be nested

---

#### Tuples

* A tuple consists of a number of values sperated by commas

* it's not possible to assign to the individual items of a tuple, but it can contain mutable objects like lists

* They are immutable themselves

```python
my_tuple = () # empty tuple
my_tuple = ('only_one_item',) # Tuple with one item
t = 1, 2, 3 # tuple packing
x, y, z = t # tuple unpacking
```

---

#### Sets

* A set is an unordered collection with no duplicate elements

```python
my_set = set() #empty set since {} is for an empty dictionary
```
* similar  to lists, set comprehensions are also possible
```python
a = {x for x in "abracadabra" if x not in 'abc'}
```
---

#### Dictionaries

* dictionaries are indexed by keys unlike sets, tuples and lists

* a key can be any immutable type aswell as strings and numbers

* It's best to think about it as an unordered set of key:value pairs, where keys within a dictionary are unique

```python
my_dict = {} # empty dictionary
{x: x**2 for x in (2, 4, 6)} # dict comprehension

dict(sape = 4139, guido = 4127, jack = 4098) 
{'sape': 4139, 'jack': 4098, 'guido': 4127}
```
* `del` can be used to delete a key:value pair
---

#### Looping

* Looping through dictionaries can be done iusing the `items()` method

```python
for a, b in my_dict.items():
    print(a, b)
```

* While looping through a squenc one can retrieve position index and the corresponding value using the `enumerate()` function

```
for a, b in enumerate(['tic', 'tric', 'trac']):
    print(i, v)
```

```python
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for a, b in zip(questions, answers):
    print('What is your {0}?  It is {1}.'.format(a, b))
```

---

#### Modules

* Each module has it's own private symbol table, which is used as the global symbol table by all functions defined in the module, so you doesn't have to worry about accidental clashes with your own global variables.

* You can import names from a module directly into the importing module's symbol tyble by using `from module_x import function_1, name_1`, but this doesnt import the module name itself

* You can use __as__ to rename the imported module or name e.g. `import networkx as nx` and `from networkx import core as c`

* From stack overflow about packages

> Any Python file is a module, its name being the file's base name without the .py extension. A package is a collection of Python modules: while a module is a single Python file, a package is a directory of Python modules containing an additional __init__.py file, to distinguish a package from a directory that just happens to contain a bunch of Python scripts. Packages can be nested to any depth, provided that the corresponding directories contain their own __init__.py file.Any Python file is a module, its name being the file's base name without the .py extension. A package is a collection of Python modules: while a module is a single Python file, a package is a directory of Python modules containing an additional __init__.py file, to distinguish a package from a directory that just happens to contain a bunch of Python scripts. Packages can be nested to any depth, provided that the corresponding directories contain their own __init__.py file.

* While importting a package module or function one has to follow the hierarchy of the package

---

#### Format

```python
print('{1} and {0}'.format('spam', 'eggs'))
spam and egg

print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
                                                       other='Georg'))
The story of Bill, Manfred, and Georg.


```

* '!a' for `ascii()`, '!s' for `str()` and '!r' for `repr()` can be used

* using __:__ can be used to format your strings better e.g. `{0:.3f}` would round py to 3 decimals after the decimal

----

#### Reading and writing files 

* `open(filename, mode)` to open a file in one of 4 modes:
    * 'r' when the file will only be read
    * 'w' for only writing
    * 'a' opens the file appending the data written to the end
    * 'r+' for both reading and writing

* It's good practice to use the with keyword when dealing with file objects, so that they are properly closed afterwards, otherwise one has to call f.close()

```python
with open('workfile') as f:
    read_data = f.read()
```

* It is rather easy to for strings and integers to read an written to a file in python, but working with mnor compley data types like dicts and lists makes it a bit more complicated. The __json__ module can take python hierarchies and convert them to string representations, called __serializing__. Reconstructing the data from the string representation is called __deserializing__.

```python
import json
json.dumps([1, 'simple', 'list']) # returns:
'[1, "simple", "list"]'
```

* `json.dump(x, f)` can be used to serialize to a text file opened for writing, in this instance f.

* This way one can handle lists and dicts, but serializing arbitrary class instances in JSON is harder.

---

#### Exceptions

* Errors detected during execution are calld __exceptions__

* There are abunch of built-in exceptions e.g. `NameError`,`TypeError`, `ZeroDivisionError`

* With the try statement you can handle exceptions:
    * first the try clause between the try and except keywords is executed
    1. If no exception occurs: the except clause is skipped
    1. If an exception occurs during execution: the rest of the try statement is skipped and if the exception matches the exception after the __except__ keyword, the except clause is executed
    1. If the exception doesn't match, it will be passed to outer try statements. If no handler is found the execution stops and the error message is shown 

* A try statement can have multiple except clauses and one except clause can handle multiple errors, given as a paranthesized tuple

* The specific error name in the last except clause can be omitted to handle a wildcard error

* There is also an optional else clause, which must follow all except clauses and is useful to specifiy what should happen if the try statement doesn't raise an exception

```python
import sys

try:
    f = open('myfile.txt')
    s = f.readline()
    i = int(s.strip())
except OSError as err:
    print("OS error: {0}".format(err))
except ValueError:
    print("Could not convert data to an integer.")
except:
    print("Unexpected error:", sys.exc_info()[0])
    raise
else:
    print('Whatever you want')
```

* The `raise` statement allows the programmert to force a specified exception to occur 

* Programmers can create their own exceptions by creating a new exception class

> When creating a module that can raise several distinct errors it is common practic to create a base class for exceptions defined by that module, and subclass that to create specific exeption classes for different error conditions

```python
class Error(Exception):
    """Base class for exceptions in this module."""
    pass

class InputError(Error):
    """Exception raised for errors in the input.

    Attributes:
        expression -- input expression in which the error occurred
        message -- explanation of the error
    """

    def __init__(self, expression, message):
        self.expression = expression
        self.message = message
```

* You can define a finally clause which is executedbefore leaving the try-statement under any cirumstances, which may be useful for releasing external resources, such as files or network connections

```python
try:
    raise KeyboardInterrupt
finally:
    print('Goodbye, world!')
```

--- 

#### Classes 

> Creating a new class creates a new type of object, allowing new instances of that type to be made

* Classes themselves are objects and and multiple names in multiple scopes canbe bound to the same object which is called aliasing in other languages

##### Scopes and Namespaces

* A __namespace__ is a mapping from names to objects. It is important to note that the names in different namespaces have nothing to do with each other, which means in different namespaces there could be the function `my_func()`

* In tne expression `modname.funcname`, `modname` is a module object and `funcname` is an attribute of it.

* Namespaces are created an different moments and have different lifetimes: 
    * built-in namespace created when the python interpreter starts up
    * global namespace or a module is created when the module definition is read in 
    * The local namespace for a function is created when the function is called and is deleted when the function returns or when an unhandled exception occured. Recursive invocations each have their own local namespace

> A __scope__ is a textual region of a python programm where a namespace is directly accessible. "Directly acessible" here means that an unqualified reference to a name attempts to find the name in the namespace.

* To rebind variables outside the innermost scope the __nonlocal__ statement can be used, if not declared nonlocal, those variables are read-only

* If the `global` statement is not used, the assignment to names always goesinto the innermost scope. Assignments do not copy data - they just bind names to objects

* Example Note: So local, nonlocal and global, are three different namespaces

```python
def scope_test():
    def do_local():
        spam = "local spam"

    def do_nonlocal():
        nonlocal spam
        spam = "nonlocal spam"

    def do_global():
        global spam
        spam = "global spam"

    spam = "test spam"
    do_local()
    print("After local assignment:", spam)
    do_nonlocal()
    print("After nonlocal assignment:", spam)
    do_global()
    print("After global assignment:", spam)

scope_test()
print("In global scope:", spam)
```

> The nonlocal statement causes the listed identifiers to refer to previously bound variables in the nearest enclosing scope. This is important because the default behavior for binding is to search the local namespace first. The statement allows encapsulated code to rebind variables outside of the local scope besides the global (module) scope.

* For a new class a new namespace is created which is used as local scope.

* Class objects support two operations: 
    * Atribute references: Here all names that were in the class's namspace when the class object was created are valid

    * Class instantiation: `x = MyClass()` creates a new instance of the class and assigns this object to the local variable x

* The only operations understood by instance objects are attribute references. There are two kind of valid attribute names, data attributes and methods.

* __Data attributes__ need to be declared like local variables e.g. `x.counter = 1`

* __methods__ are functions that belong to objects. All attributes of a class that are functions define corresponding methods for it's instances.

* the instance object is passed as the first argument of the function e.g. `x(f)` is equivalent to `MyClass.f(x)`

* The first argument of a method is calld __self__, which is just convention and doesn't mean anythin to python

* A regular method takes the instance as the first arguments

* `@classmethod` takes the class as the first argument, not the instance anymore

```python
@classmethod
def set_raise_amt(cls, amount):
    cls.raise_amt = amount
```

* classmethods can bes used as alternative constructers
```python
@classmethod
def from_string(cls, emp_str):
    first, last, pay = emp_str.split('-')
    return cls(first, last, pay)
```

* static methods don't pass in an instance or a class as the first arguments, but they still have a logical connection to the class

```python
@staticmethod
def is_workday(day):
    if day.weekday() == 5 or day.weekday() == 6:
        return False
    return True
```

* If a subclass tries to expand the `__init__` method, you don't have to typethe whole method again but can us `super().__init__(first, last, pay)`. Now you can expand on that init in any way you want.

```python
class Dog:

    def __init__(self, name):
        self.name = name
        self.tricks = []    # creates a new empty list for each dog

    def add_trick(self, trick):
        self.tricks.append(trick)
```

* The `__init__()` is used to give the created instances a wanted initialstate (__instance variables__)

* __class variables__ are set at the top of the class and can be accessed from the class and the instances

```python
class DerivedClassName(BaseClassName):
    <class text>
# if the base class is defined in another module
class DerivedClassName(modname.BaseClassName):
    <class text>
```

* If a requested attribute is not found in the derived class the search proceeds in the base class

* Derived classed may override methods of their base classes

```python
class DerivedClassName(Base1, Base2, Base3):
    <class stuff>
```

* An attribute is first searched for in DerivedClassName, after that in Base1 and then in the base classes of Base1 and so on.

* Dynamic ordering is necessary since a parent class may be accessible over multiple paths.

##### Private variables

* A name preficed with an underscore should be treated as a non-bublic part of the API(whether it is a function, a method or a data member) e.g. `_spam`

> Use one leading underscore only for non-public methods and instance variables.

> To avoid name clashes with subclasses, use two leading underscores to invoke Python's name mangling rules.

* `@property` lets us a function, just like an attribute and to access that properly we can use a sett or even a deleter if we wanted to

```python
class Employee():
    @property
    def fullname(self):
        return '{} {}'.format(self.first, self.date)

@fullname.setter
def fullname(self, name):
    first, last = name.split(' ')
    self.first = first
    self.last = last

@fullname.deleter
def fullname(self):
    print('Delete Name!')
    self.first = None
    self.last = None
```

---

#### Magic/Dunder Methods

 * With those we can change built in behavior and operations e.g. printing and instance gives us a memoryadresse, but it would be nice to see something more user friendly

* `__repr__` is an an unambiguous (eindeutig) representation of an object used for debugging, logging and is meant to be seen by other developers

```python
class Employee():
    def __repr__(self):
        return "Employee('{}', '{}', '{}'.format(self.first, self.last, self.pay))"
```

* `__str__` is meant to be a readably represenation of an object and is meant to be used as a display to the end user

```python
class Employee():
    def __str__(self):
    return '{} - {}'.format(self.fullname(), self.mail)
```

* Both of these methos allow us to change the representation of our objects

```python
class Employee():
    def __len__(len):
    return len(self.fullname())
```

---

#### if __name__ == '__main__'

```python
def main():
    pass
if __name__ == '__main__':
    main()
```

* Befor python runs a file it sets some special variables and one of those variables is `__name__` and if python runs the file directly in sets the `__name__` as `__main__`

* When importing modules it sets the `__name__` as the modules name and not `__main__`, so we know it's run from import

* This is used because sometimes there is code you only want to run if whenever you`re running it as the main file and sometimes there is code you only want to run if it is run through import


---

#### Iterators

* The for statement calls iter() on the container object, this function returns an iterator object which defines the method __next__().This function accesses the elements in the container one at a time until der are nor more and StopIteration exception is raised which tells the for loop to stop.

* Now defining `__iter__()` and `__next__()` methods in your class you can easily add iterator behavior to your classes

```python
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]
```
---

#### Generators

* Generators are a mechanism by which you can create code, that can interleave with other code and also inforce sequencing

* Generators are a simple and powerful tool to creat iterators

* __yield__ gives us a generator object

* Using genrators is compact because `__iter__()` und `__next__()` are created automatically, so the last example would look like this:

```python
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]
```

* local variables and execution state are automatically saved between calls

* You can create generators just like list comprehensions by using parentheses () instead of brackets [] e.g. `my_nums = (x*x for x in [1, 2, 3, 4, 5])`

* A generator yields better performance then lists since it doesn't hold every items in memory. Really noticeable for a huge amount of elements. 'Casting' a generator to a list loses all the performance gains --> safes time and memory

---

#### Virtual Environments

* Some python applications may need certain library versions so one Python installation may not meet the requirements for all of the applications.

* In that case we can create a virtual-environments which is a self contained directory tree that contains a particular version of python. So different applications can use different virtual environments

```
pip install virtualenv
# Make a Directory for all the environments for better overview
virtualenv project1_env # Creation

project1_env\Scripts\activate.bat # windows activate
source project1_env/bin/activate # Unix or MacOS activate

which pyhon # shows us where our python is located
python --version

pip list # to see what king of packages we have in our environments

pip freeze --local > requirements # safe package reqs. in a file

pipi install -r rquirements.txt

deactivate # leave your current environment

virtualenv -p /usr/bin/python2.6 py26_env # create env with a certain python version
```

* Don't save your poject files in those environments directories

---

#### Decorators

##### Closures

> A closure is an inner function that remembers and has access to variables in the local scope in which it was created even after the outer function has finished executing

```python
def outer_function(msg):
    def inner_function():
        print(msg)
    return inner_function # returning Function waiting to be executed

hi_func = outer_function('Hi') # Variable is actually function in thise case the inner_func function `print(hi_func.__name__)`
bye_func = outer_function('Bye')

hi_func() # --> Hi
bye_func() # --> Bye

```

> There are a lot of usecases for something like this. It's especially useful for when you want to add or alter the functionality of your functions, without altering the code of the functions themselves. So for example, in this video I added logging capabilities to the add and subtract functions, all without adding any logging code to those functions themselves. This allows us to keep all of the logic separated into their own specific functions. If you'd like to read more about it, I would suggest looking up "Aspect Oriented Programming". You will see a few more useful examples there.

##### First Class Functions

* We should be able to use functions like any attribute of object

```python
def square(x):
    return x * x

f = square # without the parentheses the function is not executed
```

* If a function accepts other functions as arguments or returns functions as their results, that's what you call a higher order function

```python
def decorator_function(original_function):
    def wrapper_function(*args, **kwargs):
        print('wrapper executed this befor {}'.format(original_function.__name__))
        # we need thos arguments if the function we want to decorate takes additional arguments
        return original_function(*args, **kwargs)
    return wrapper_function

@decorator_function # --> equal to display = decorator_function(display) "I want my following function to be equal to the ecorator function with my display function passed in" 
def display():
    print('display function ran')

@decorate_function
def display_info(name, age):
    print('display_info ran with arguments ({}, {})'.format(name, age))

display() # with the @ syntax we can the code below just like this
#decorated_display = decorator_function(display)
#decorated_display()
```

* Decorating our function lets us easily add functionality to our existing functions, by adding that functionality inside our wrapper

* You can use a class to decorate like this:
```python
class decorator_class(object):
    
    def __init__(self, original_function)
        self.original_function = original_function

    def __call__(self, *args, **kwargs):
        print('call method executed this befor {}'.format(self.original_function.__name__))
        return self.original_function(*args, **kwargs)
```

* Typical applications are logging and timing 

* You can add two decorators to a function by simply stacking them on top of each other equvalent to `display_info_func = decorator_1(decorator_2(display_info_func))`. So the lower decorators on the stack get executed first. In this case the outer decorator is given the wrapper function, which doesn't do what we want.

* `from functools import wraps` for every wrapper of our decorators we just add the wraps decorator `@wraps(input_function)`

* Decorators are simple syntax that allows us to write an ugly pattern, that allows us this wrapping behavior for functions to add functionality in one place without having to rewrite a lot of user code or even perform a lot of churn on your library code

---

#### Unit Testing

```python
import unittest 
import calc # module we want to test

class TestCalc(unittest.TestCase):
    @classmethod
    def setUpClass(cls): # gets run once before everything
        print('setupClass')
    @classmethod # gets run once after everything
    def tearDownClass(cls):
        print('teardownclass')
    def setUp(self): # run it's code before every single test
        self.emp1 = Employee('Corey', 'Schafer', 5000)
        # Employee gets created before every single test which helps to keep the code dry, since we dont't have to create them in every test function indiviually

    def tearDown(self): # run after every single test
        pass
    # Coul be useful for instance when you have a function that added files to a database, so you could create that database in your setUp method and delete the files in the tearDown method
    def test_add(self): # test function has to start with 'test_'
        self.assertEqual(calc.add(10, 5), 15)

if __name__ == '__main__':
    unittest.main()
```

* If we have a function that downloads something from a website and that website is down the test will fail even if your code is working

```python
from unittest.mock import patch

class TestCalc(unittest.TestCase):
    
    def test_monthly_schedule(self):
        with patch('employee.requests.get') as mocked_get:
            mocked_get.return_value.ok = True
            mocked_get.return_value.teyt = 'Success'

            schedule = self.emp_1.monthly_schedule('May')
            moked_get.assert_called_with('http://company.com/Schafer/may')

```

* Tests don't necessarily run in order

* __Test Driven Developement__: Write Tests and then the code itself

---

#### Context Manager

* Are a structure that allow you to tie two actions together:
    * setupaction
    * teardownaction

```python
from sqlite3 import connect
from contextlib import contextmanager

@contextmanager
def template(curl):
    cur.execute('create table points(x int, y int)')
    try:
        yield
    finally
        cur.execute('drop table points')
```


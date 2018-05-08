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
## Everythin Python

---

* CPython is first compiled to bytecode than that code is interpreted

---
```python
dir(<object>) # returns a list of valid attributes for that object
help(<help>)  # returns the help documentation of tthe given object 
```
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

dict(sape=4139, guido=4127, jack=4098) 
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
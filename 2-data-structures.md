# Data Structures
Data structures might not be the sexiest topic but they're a crucial part of programming in general and have some deep insights into Python's language design.

Lists, tuples, and sets all store collections of objects and dictionaries store mappings (with key-value pairs).

## Lists
We've already seen lists in Python! They are finite, ordered, mutable, collections of elements.

* Finite – lists have a non-infinite size.
* Ordered – every element in a list has an index and the elements have an order (there is a first element, second element, third element, etc.).
* Mutable – after a list is created, you can modify it.

Lists are delimited with square brackets (`[]`) and commas separate elements. So, `simple_as = ['do', 're', 'mi']` defines a list that contains three elements.

Lists can contain any type of object. One list can also have elements of different types. For example,

```python
mixed = [4, 5, 'seconds']
inception = [['a', 'dream'], ['within', 'a'], 'dream']
```

As we mentioned in [Python Basics](1-python-basics.md), list indexing and slicing behaves similarly to strings. 

To get the number of elements in a list, use the `len` function. For example,

```python
len(inception) # => 3
```

You can also check if an element is in a list with the `in` keyword. For example,

```python
'within' in inception        # => False
['within', 'a'] in inception # => True
```

You can convert other collections into lists using the `list` function. For example, a string is a collection of characters; we can produce a list of characters from a string like so:

```python
list("unicorn") # => ['u', 'n', 'i', 'c', 'o', 'r', 'n']
```

Next, we'll cover some operations that you can perform on lists which are divided into three categories – those that are very important to know, those that are good to know, and those that are less important.

| Very Important | Good to Know | Less Important |
| -------------- | ------------ | -------------- |
| `.append`      | `.extend`    | `.reverse`     |
| `.sort`        | `.count`     | `.insert`      |
| `.remove`      |              |                |

### Very Important
`.append` allows you to add an element to the end of a list. For example,

```python
numbers = [2, 3, 5, 5]

numbers.append(4)
numbers # => [2, 3, 5, 5, 4]
```

`.sort` allows you to sort a list in place (the function returns `None`, but the value of the list will change). Continuing the previous example,

```python
numbers.sort()
numbers # => [2, 3, 4, 5, 5]
```

Finally, `.remove` allows you to remove the first instance of an element by value. For example,

```python
numbers.remove(5)
numbers # => [2, 3, 4, 5]
```

If you try to remove an element that doesn't exist in the list, the program will raise a `ValueError`.

### Good to Know
If you want to append a series of numbers that are stored in another list (more precisely, any ordered collection), you can use the `.extend` function. For example,

```python
letters = ['u', 'n', 'i', 'c', 'o', 'r', 'n']

numbers.extend(letters)
numbers # => [2, 3, 4, 5, 'u', 'n', 'i', 'c', 'o', 'r', 'n']
```

The `.count` function returns the number of occurrences of an element in a list. For example,

```python
letters.count('n')             # => 2
letters.count(['u', 'n', 'i']) # => 0
```

### Less Important
The `.reverse` function will reverse the order of a list in place (the function will return `None` but the value of the list will change). For example,

```python
letters.reverse()
letters # => ['n', 'r', 'o', 'c', 'i', 'n', 'u']
```

Finally, the `.insert` function will add an element into a list at a location other than the end of the list. You provide two arguments to the `.insert` function: an index and the element to insert. For example,

```python
letters.insert(1, True)
letters # => ['n', True, 'r', 'o', 'c', 'i', 'n', 'u']
```

## Tuples
Tuples are virtually identical to lists except for the fact that tuples are immutable. This means that after a tuple is created, it cannot be modified.

This feature has a plethora of benefits. For one, Python has decided that because of this, tuples can be hashable which allows them to serve as keys in a dictionary. More broadly, tuples should be used to represent data which has a fixed number of entries.

A tuple is declared with parenthesis and commas separating elements. **Warning**: To create a tuple with one element, you have to add a comma after the element. For example,

```python
t = (4)
type(t) # => int

t = (4,)
type(t) # => tuple
```

One good use of tuples is to represent an addresses. For example,

```python
sherlock = ('221B Baker St', 'London', 'UK')
```

In the above representation, we've decided that an address will be represented by `(street, city, country)`. It doesn't make sense to "append" or "delete" an element from an address so it's better to use a tuple rather than a list.

If you try to edit an element of a tuple, Python will raise a `TypeError`. For example,

```python
sherlock[0] = '221C Barker Ln' # TypeError
```

But you can use the `len` function, the `in` keyword, and slicing/indexing just like lists. For example,

```python
len(sherlock)    # => 3
'UK' in sherlock # => True
sherlock[::-1]   # => ('UK', 'London', '221B Baker St')
```

### Tuple Packing
Tuple packing and unpacking are two of the most innocuous-looking but powerful features of Python.

If you type a series of objects separated by commas, Python will automatically bundle them together into a tuple. This is called tuple packing. For example,

```python
christopher_robin = 'Pooh', 'Tigger', 'Piglet'
print(christopher_robin) # ('Pooh', 'Tigger', 'Piglet')
type(christopher_robin)  # tuple
```

If you type a series of variable names and set them equal to a tuple, Python will assign values to the variables element by element. This is called tuple unpacking. For example,

```python
x, y, z = christopher_robin

x # => 'Pooh'
y # => 'Tigger'
z # => 'Piglet'
```

These two can be used in tandem if you'd like to assign values to multiple variables at the same time. For example,

```python
first, last, age = 'Unicornelius', None, 1001
```

You can also swap the values of two variables really succinctly:

```python
first, last = last, first

first # => None
last  # => 'Unicornelius'
```

For example, we can use tuple unpacking to succinctly compute the fibonacci series:

```python
def fibbi(n):
    """
    Print out the first n Fibonacci numbers
    """
    a, b = 0, 1
    
    for i in range(n):
        print(a)
        a, b = b, a + b
```

### Immutable References
One quirk of tuples is that you can put a mutable object into a tuple! For example,

```python
org = ("Dumbledore's Army", ['harry', 'hermione', 'ron'])
```

Tuples contain immutable references to underlying objects, even if those objects are mutable. For example, we could do:

```python
org[1].append('cho')

org # => ("Dumbledore's Army", ['harry', 'hermione', 'ron', 'cho'])
```

But, it's invalid to replace the list entirely:

```python
org[1] = ['draco', 'goyle'] # TypeError
```

## Sets
Sets are finite, distinct, mutable collections of objects but they are unordered – this is because sets can only contain hashable objects. A set in Python is roughly equivalent to a `HashSet` in Java.

Sets are distinct, meaning that they can't contain multiple copies of the same element (unlike lists and tuples).

Sets are delimited with squiggly brackets (`{}`) and elements of a set are separated with commas. For example,

```python
students = {'Guido', 'Parth', 'Unicornelius'}
```

Sets are useful for three main reasons:

1. Membership testing is fast – it's very quick ($O(1)$) to test if an element is in a set.
2. Eliminating duplicates is easy – if you'd like to remove duplicate elements from a collection of hashable objects, you can put them into a set to quickly and easily remove duplicate entries.
3. Mathematical set operations – it's really easy to perform mathematical operations on Python sets (like taking the intersection of two sets).

You can create an empty set with the `set` function like so:

```python
empty_set = set()
```

You cannot set `empty_set = {}` because that would create an empty dictionary (next section). The `set` function is also used to convert other collections to sets like so:

```python
set_from_list = set([1, 2, 1, 4, 3])
set_from_list # => {1, 2, 3, 4}
```

Many of the previous operations on collections apply to sets as well. You can return the number of elements in a set with `len`, check if an element is in a set with the `in` keyword, and iterate over a set with `for`.

For example,

```python
basket = {'orange', 'banana', 'pear', 'apple'}

len(basket)           # => 4

'orange' in basket    # => True
'crabgrass' in basket # => False

for fruit in basket:
    print(fruit)

# apple
# banana
# pear
# orange 
```

### Set Methods

To add an element to a set, use the `.add` method. For example,

```python
letters = set('mississippi')
letters # => {'i', 'm', 'p', 's'}

letters.add('unicorn')
letters # => {'i', 'm', 'p', 's', 'unicorn'}
```

To remove an element, use the `.remove` method. This method will raise a `KeyError` if you ask it to remove something that's not in the set. For example,

```python
letters.remove('m')
letters # => {'i', 'p', 's', 'unicorn'}
```

You can also remove all the elements from a set with the `.clear` method (like `st.clear()`) but this isn't frequently used.

### Mathematical Set Operations

You can perform a lot of mathematical operations on sets which integrate with Python operators. First, let's define:

```python
a = set('abracadabra') 
b = set('alacazam')

a # => {'a', 'r', 'b', 'c', 'd'}
b # => {'a', 'm', 'c', 'l', 'z'}
```

To take the difference between two sets use the minus (`-`) operator. For example, `a - b` will return the elements that are in `a` but not in `b`:

```python
a - b # => {'b', 'd', 'r'}
```

You can take the union of two sets using the pipe (`|`) operator. `a | b` will return a set containing elements that are in `a` or in `b`. In particular,

```python
a | b # => {'a', 'b', 'c', 'd', 'l', 'm', 'r', 'z'}
```

And, you can take the intersection of two sets using the ampersand (`&`) operator. `a & b` returns a set with elements that are in `a` and `b`. In particular,

```python
a & b # => {'a', 'c'}
```

You can also combine any of these operations with `=` to update the value of `a`. For example, `a |= b` is roughly equivalent to `a = a | b`.

### Mathematical Set Comparisons

The mathematical comparison operators (`<`, `<=`, `>`, `>=`) make sense in the context of sets as well. They test set containment.

That is, `a < b` is `True` if `a` is a subset of `b`. `a <= b` is `True` if `a` is a subset of or equal to `b`. The meanings of `>` and `>=` are reversed.

## Dictionaries
## Comprehensions
## Advanced Looping

> With love and 🦄s by @psarin and @coopermj
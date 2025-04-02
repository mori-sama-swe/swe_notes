# Dictionaries In Python

## Understanding Dictionaries in Python

In Python, a **dictionary** is a collection of key-value pairs. It’s like a real-world dictionary where words (keys) are mapped to their meanings (values). 

Dictionaries are **unordered** (though they preserve insertion order since Python 3.7), **mutable** (can be changed after creation), and highly efficient for lookups. 

- This guide will cover how to create, access, and manipulate dictionaries, their methods, performance, usage examples, and how to loop through them, with all code examples in code blocks.

> [!note]
>
> Dictionaries in Python are powerful tools for storing and manipulating key-value pairs. They offer **O(1) average time complexity** for lookups, insertions, and deletions, 
>
> making them efficient for a wide range of applications. With methods like keys(), values(), and items(), along with flexible looping options and comprehensions, dictionaries are a cornerstone of Python programming. 
>
> Whether you’re counting frequencies, storing structured data, or mapping unique identifiers, dictionaries provide a fast and intuitive solution.

### Creating Dictionaries

You can create a dictionary in several ways:

**Using curly braces {}**:

```cpp
my_dict = {'apple': 1, 'banana': 2, 'cherry': 3}
```

**Using the dict() constructor**:

```python
my_dict = dict(apple=1, banana=2, cherry=3)
```

**Starting with an empty dictionary and adding items**:

```python
my_dict = {}
my_dict['apple'] = 1
my_dict['banana'] = 2
my_dict['cherry'] = 3
```

> [!important]
>
> **Keys must be immutable**: Keys can be strings, numbers, or tuples, but not lists or other dictionaries (because they are mutable).
>
> ```python
> my_dict = {(1, 2): 'point'}  # Valid
> print(my_dict[(1, 2)])       # Output: point
> # my_dict = {[1, 2]: 'list'}  # Invalid: TypeError
> ```
>
> **Dictionaries are mutable**: Assigning a dictionary to a new variable creates a reference to the same object.
>
> ```python
> dict1 = {'a': 1}
> dict2 = dict1
> dict2['a'] = 2
> print(dict1['a'])  # Output: 2
> ```
>
> - To create an independent copy, use the **copy() method:**
>
>   ```python
>   dict1 = {'a': 1}
>   dict2 = dict1.copy()
>   dict2['a'] = 2
>   print(dict1['a'])  # Output: 1
>   ```
>
>   

---
### Accessing Dictionary Elements

You access values in a dictionary using their keys:

**Using square brackets []**:

> [!warning]
>
> **If the key doesn’t exist, this raises a KeyError.**

```python
print(my_dict['apple'])  # Output: 1
```

**Using the get() method** (safer option):

```python
print(my_dict.get('orange'))      # Output: None
print(my_dict.get('orange', 0))   # Output: 0 (default value if key not found)
```

---

### Dictionary Methods

1. `dict.keys()` - returns a view of all the keys in the dictionary

```python
my_dict = {'apple': 1, 'banana': 2, 'cherry': 3}
keys = my_dict.keys()
print(keys)  # Output: dict_keys(['apple', 'banana', 'cherry'])
```

![image-20250330235628289](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/image-20250330235628289.png)

2. `dict.values()` - returns a view of all values in the dictionary

```python
my_dict = {'apple': 1, 'banana': 2, 'cherry': 3}
values = my_dict.values()
print(values)  # Output: dict_values([1, 2, 3])
```

3. `dict.item()` - returns a view of all key-value pairs as `tuples`
   - Perfect for looping over both keys and values at the same time.

```python
my_dict = {'apple': 1, 'banana': 2, 'cherry': 3}
items = my_dict.items()
print(items)  # Output: dict_items([('apple', 1), ('banana', 2), ('cherry', 3)])
```

![image-20250331000015115](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/image-20250331000015115.png)

4. `update()` - Updates the dictionary with key-value pairs from another dictionary or iterable.

```python 
my_dict = {'apple': 1, 'banana': 2}
my_dict.update({'cherry': 3, 'date': 4})
print(my_dict)  # Output: {'apple': 1, 'banana': 2, 'cherry': 3, 'date': 4}
```

5. `dict.get( )` - returns the value for a specified key, or a default value if the key does not exist
   - This avoids errors by providing a fallback when a key is missing.

```python
my_dict = {'apple': 1, 'banana': 2}
value = my_dict.get('cherry', 0)
print(value)  # Output: 0
```

6. `setdefault()` - Returns the value of a key if it exists; otherwise, inserts the key with a default value.

```python
my_dict = {'apple': 1}
value = my_dict.setdefault('banana', 2)
print(value)    # Output: 2
print(my_dict)  # Output: {'apple': 1, 'banana': 2}
```



---

## How To Use Dictionaries

Dictionaries are versatile and can be used in many ways. Here are two common examples:

Examples:

1) **counting frequencies**

```python
words = ['apple', 'banana', 'apple', 'cherry', 'banana', 'apple']
frequency = {}
for word in words:
    frequency[word] = frequency.get(word, 0) + 1
print(frequency)  # Output: {'apple': 3, 'banana': 2, 'cherry': 1}
```

2. storing structured data (nested dictionaries )

```python
users = {
    'user1': {'name': 'Alice', 'age': 30},
    'user2': {'name': 'Bob', 'age': 25}
}
print(users['user1']['name'])  # Output: Alice
```

---

## Performance of Dictionaries

Dictionaries in Python are implemented as **hash tables**, which makes them highly efficient:

- **Average time complexity** for lookups, insertions, and deletions is **O(1)**.
- In rare cases (due to hash collisions), performance can degrade to **O(n)**, but this is uncommon.
- This efficiency makes dictionaries ideal for scenarios requiring fast access to data by key.

---

## Looping Through Dictionaries

### Looping In General

**Looping through keys and values (default behavior):**

```python
for key in my_dict:
    print(key, my_dict[key])
    
    
for value in my_dict.values():
    print(value)
```

**Looping through key-value pairs**:

```python
for key, value in my_dict.items():
    print(key, value)
```

### `items ()` and why its good for looping

its good for looping since we have direct access to Key-Value Pairs

> [!note]
>
> A Python dictionary stores data as key-value pairs, such as {'apple': 2, 'banana': 3, 'cherry': 1}. The items() method returns a view of these pairs as tuples, like [('apple', 2), ('banana', 3), ('cherry', 1)]. 
>
> **When you loop over items(), you can unpack each tuple** 

```python
cart = {'apple': 2, 'banana': 3, 'cherry': 1}
for product, quantity in cart.items():
    print(f"{product}: {quantity}")'
    
output:
apple: 2
banana: 3
cherry: 1
```

Compare this to looping over just the keys:

```python
for product in cart:
    quantity = cart[product]
    print(f"{product}: {quantity}")
```

> [!important]
>
> Without items(), **you need an extra lookup (cart[product]) inside the loop to get the value, which adds a step**. With items(), you get both the key and value in one go, simplifying the process.

> [!note]
>
> Performance-wise, items() is efficient. **Looping over keys and doing lookups (e.g., dict[key]) is an O(1) operation per lookup due to dictionaries being hash tables, so for *n* keys, the total time is O(*n*). Using items() is also O(*n*), but it avoids the overhead of repeated lookups by providing the key-value pairs directly.** 
>
> While the difference might be small for small dictionaries, items() is implemented efficiently in Python’s C backend, making it a streamlined choice.

> [!warning]
>
> **One thing to note: avoid modifying the dictionary (e.g., adding or removing keys) while looping over items(), as it can cause errors or unexpected behavior.** For safe modifications, consider collecting changes separately and applying them after the loop.

## Nested Dictionaries

> [!NOTE]
>
> A **nested dictionary** is a dictionary inside another dictionary. It allows you to organize complex data in a hierarchical way.
>
> ```python
> students = {
>     'student1': {
>         'name': 'Alice',
>         'age': 22,
>         'grades': {'math': 90, 'english': 85}
>     },
>     'student2': {
>         'name': 'Bob',
>         'age': 24,
>         'grades': {'math': 75, 'english': 92}
>     }
> }
> 
> # Accessing nested data
> print(students['student1']['grades']['math'])  # Output: 90
> ```

### Accessing Nested Dictionaries

```python
print(person["address"]["city"])  # Output: Springfield
```

### Looping Through Nested Dictionaries

```python
for key, value in person.items():
    if isinstance(value, dict):
        for subkey, subvalue in value.items():
            print(f"{key} -> {subkey}: {subvalue}")
    else:
        print(f"{key}: {value}")
```



## Dictionary Comprehensions

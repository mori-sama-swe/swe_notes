# Python Data Types

## Variables

A **variable** in Python is a named location in memory that holds a value. It acts as a reference to an object (like a number, string, or list) stored in memory.

> [!note]
>
> Summary:
>
> - **Declaration**: Occurs automatically when you assign a value to a variable for the first time.
> - **Initialization**: Done using the = operator to assign an initial value.
> - **Dynamic Typing**: Variables can switch types by reassigning values of different types.
> - **Naming**: Must follow specific rules and avoid reserved keywords.
> - **Scope**: Can be local (inside functions) or global (outside functions).
> - **Deletion**: Use del to remove a variable.

> [!note]
>
> **Variable Naming Rules:**
>
> - Must start with a letter (a-z, A-Z) or an underscore _.
> - Can contain letters, numbers (0-9), and underscores _.
> - Are **case-sensitive** (e.g., age and Age are different variables).
> - Cannot be Python reserved keywords (e.g., if, for, class).


### Declaration of Variables in Python

- **No explicit declaration**: In Python, you don’t need to declare a variable before using it, as you would in languages like C or Java. Instead, a variable is created the moment you assign a value to it.
- **How it works**: Declaration and initialization happen together when you first assign a value to a variable name.
  - whenever a  variable is declared it should be initialized. **Declaration and  initialization is done together.. a variable cannot be left blank**

```python
x = 5  # This declares the variable 'x' and assigns it the value 5
```

Here, x is automatically declared as a variable when it’s assigned the integer 5. Python infers its type based on the value.

### Initialization of Variables In Python

**Initialization**: This is the process of assigning an initial value to a variable. In Python, you use the assignment operator `=` to do this.

```python
name = "Alice"  # Initializes 'name' with the string "Alice"
age = 30        # Initializes 'age' with the integer 30
score = 95.5    # Initializes 'score' with the float 95.5
```

#### Multiple Assignment

Python allows you to assign values to multiple variables in a single line.

```python
x, y = 5, 10  # Initializes x to 5 and y to 10
```

### Variable Scope

**Variables** in Python have a scope, which determines where they can be accessed:

- **Local variables**: Defined inside a function and only accessible within that function.

- **Global variables**: Defined outside any function and accessible throughout the program.

```python
global_var = "I am global"

def my_function():
    local_var = "I am local"
    print(global_var)  # Works: "I am global"
    print(local_var)   # Works: "I am local"

my_function()
print(global_var)  # Works: "I am global"
# print(local_var)  # Error: local_var is not accessible here
```

### Deleting Variables

You can remove a variable using the del statement, which unbinds the variable name from its value.

```python
x = 5
del x  # Deletes the variable 'x'
# print(x)  # Error: x is no longer defined
```

----

## Python DataTypes

Python has several built-in data types that are essential for programming. Below is a detailed breakdown of the main data types, their characteristics, and examples of how to use them.

> [!important]
>
> 

![image-20250330222352969](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/image-20250330222352969.png)

### Numeric

**int** (Integer): Whole numbers without a decimal point.

**float** (Floating-Point): Numbers with a decimal point.

**complex** (Complex Numbers): Numbers with real and imaginary parts.

```python
x = 5          # Positive integer
y = -3         # Negative integer
z = 1000       # Large integer

a = 3.14       # Positive float
b = -0.001     # Negative float
c = 2.0        # Float with no decimal value

d = 3+4j       # Real part: 3, Imaginary part: 4
e = -2-5j      # Real part: -2, Imaginary part: -5
```

----

### Sequence Types

Sequence types in Python are ordered collections of items. Each item has an index (starting at 0), and they can be accessed by their position.

- they are accessed via `Index`

> [!NOTE]
>
> **Visualizing the Structure**
>
> If you imagine these as boxes in a row:
>
> - **String**: A row of boxes, each containing a single character.
> - **List**: A row of boxes, each containing any type of item, and you can swap out the contents.
> - **Tuple**: A row of boxes, each containing an item, but the boxes are "locked" (immutable).

```python
# String
s = "hello"
# Diagram representation: "h" (0), "e" (1), "l" (2), "l" (3), "o" (4)

# List
l = [1, "two", 3.0]
# Diagram representation: 1 (0), "two" (1), 3.0 (2)

# Tuple
t = (10, 20, 30)
# Diagram representation: 10 (0), 20 (1), 30 (2)
```

**str** (String): A sequence of characters.

```python
s1 = "hello"   # Using double quotes
s2 = 'world'   # Using single quotes
```

**list**: An ordered, **mutable** collection of items.

```python
l1 = [1, 2, 3]           # List of integers
l2 = ["a", "b", "c"]     # List of strings
l3 = [1, "hello", 3.14]  # Mixed types
```

**tuple**: An ordered, **immutable** collection of items.

```python
t1 = (1, 2, 3)           # Tuple of integers
t2 = ("a", "b", "c")     # Tuple of strings
t3 = (10, 20)            # Tuple for coordinates
```

### Set Types

These are unordered collections of unique items.

**set**: A mutable collection of unique elements.

```python
set1 = {1, 2, 3}         # Set of integers
set2 = {"a", "b", "c"}   # Set of strings
set3 = {1, 1, 2}         # Duplicates removed, becomes {1, 2}
```

**frozenset**: An immutable version of a set.

```python
fs = frozenset([1, 2, 3])  # Immutable set
```

### Dict (Mapping Types)

These store data as key-value pairs, **dict** (Dictionary): An unordered collection of key-value pairs.

accessed via `key` 

```python
d1 = {"key1": "value1", "key2": "value2"}  # Simple dictionary
d2 = {"name": "Alice", "age": 30}          # Dictionary with mixed value types
```

----

## Type Conversions

> [!note]
>
> **Key Considerations**
>
> - **Data Loss**: Converting from float to int (e.g., int(3.9) → 3) loses the decimal part.
>
> - **Invalid Conversions**: Attempting int("abc") or float("xyz") raises a ValueError.
>
> - Operator Behavior
>
>   : The 
>
>    operator adds numbers but concatenates strings. Type matters!
>
>   - 5 + 3 → 8 (integer addition).
>   - "5" + "3" → "53" (string concatenation).

### Implicit Type Conversion

**Implicit Type Conversion:**

Python sometimes converts types automatically to avoid data loss or to make operations possible. This happens without explicit instructions from the programmer.

- **How it works**: Python promotes a "smaller" type (e.g., integer) to a "larger" type (e.g., float) when needed.

- **Common scenario**: Arithmetic operations involving mixed types.

```python
x = 5      # integer
y = 2.5    # float
z = x + y  # Python converts 5 to 5.0, then adds
print(z)   # Output: 7.5 (float)
```

**Explicit Type Conversion**

When you need to manually convert a value to a specific type, Python provides built-in functions. These are the most common ones:

example:

 **int() - Converts to Integer**

- Converts floats, strings, or booleans to an integer.
- For floats, it truncates the decimal part (rounds toward zero).
- For strings, the string must represent a valid integer (e.g., "123", not "12.3").

```python
print(int(3.7))     # Output: 3 (truncates decimal)
print(int("123"))   # Output: 123
print(int(True))    # Output: 1 (True is 1, False is 0)
print(int("12.3"))  # Error: ValueError (invalid literal)
```


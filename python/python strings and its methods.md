# Understanding String Class and Its Methods

## String Representation

Python strings can be understood and represented similarly to arrays (or sequences), although internally they are more complex. Here's a clear elaboration for your notes:

In Python, a string is essentially an **immutable sequence** of Unicode characters. While Python doesn't explicitly call them "arrays," strings behave very much like arrays because:

- **Indexed Access:** You can access each character by its index (starting from 0):

  ```python
  s = "hello"
  print(s[0])  # prints 'h'
  print(s[1])  # prints 'e'
  ```

- **Iterability:** You can iterate through each character easily:

  ```python
  for char in "world":
      print(char)
  ```

- **Slicing:** Python strings support slicing operations, just like arrays:

  ```python
  s = "hello"
  print(s[1:4])  # prints 'ell'
  ```

---

## Index Slicing

```python
#syntax python
string[start:end:step]
```

`start`: Index where the slice starts (inclusive). Defaults to `0` if omitted.

`end`: Index where the slice ends (exclusive). Defaults to the end of the string if omitted.

`step`: Interval between characters. Defaults to `1` if omitted.

![image-20250401215119439](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/image-20250401215119439.png)

### Basic Slicing 

```python
s = "Hello"
# start:end
s[0:5]  # "Hello - Characters from index 0 (inclusive) to 5 (exclusive).

# :end
s[:5]   # "Hello" - Starts from the beginning (index 0 by default).

#start: 
s[7:]   # "World!" - From index 7 to the end of the string.
```

### Negative Slicing 

Negative indices start from the end (`-1` is last character):

```python
s[-6:-1]  # "World"
s[::2]    # "Hlo ol!"
s[::-1]   # "!dlroW ,olleH"
```

> [!important]
>
> ```python
> ### Slice	Meaning	Example (s="Hello")	Result
> s[start:end]	From start (inclusive) to end (exclusive)	s[1:4]	"ell"
> s[:end]	From start to end	s[:3]	"Hel"
> s[start:]	From start to end	s[2:]	"llo"
> s[start:end:step]	With interval step	s[::2]	"Hlo"
> s[::-1]	Reverse string	s[::-1]	"olleH"
> ```

### Difference Between 

> [!note]
>
> text = "Python"
>
> print(text[0])  # Output: P
> print(text[-1])  # Output: n
>
> print(text[0:4])  # Output: Pyth
> print(text[2:])   # Output: thon
> print(text[:2])   # Output: Py

### Performance Consideration :

- **Strings in Python are immutable**, and slicing creates a new string.
  - `slicing` creates a shallow copy (new memory instance)
- Frequent slicing of very large strings can lead to higher memory usage and reduced performance.

---

## find( ) and index( ) method

`find( )` - method searches for a substring within a string and returns the **lowest index** (position) of the substring. If the substring is **not found**, it returns `-1`.

````python
# syntax
str.find(substring, start, end)
````

`substring`: Required. The string you're looking for.

`start`: Optional. Index to start the search (default is 0).

`end`: Optional. Index to end the search (default is end of string).

Example:

```python
text = "hello world"
print(text.find("world"))  # Output: 6
print(text.find("python")) # Output: -1 
```

`index( ) method` - The `index()` method is very similar to `find()`. It returns the lowest index (position) of the substring, but if the substring is **not found**, it raises a `ValueError`.

```python
#syntax
str.index(substring,start,end)
```

Example:

```python
text = "hello world"
print(text.index("world"))  # Output: 6

# Raises ValueError
print(text.index("python")) 

# output:
ValueError: substring not found
```

> [!note]
>
> **When to use each?**
>
> - Use `find()` when you need to handle the possibility that the substring might **not exist**. It's safer because you can easily handle the `-1` result with conditional statements.
> - Use `index()` when you expect the substring **to be present** and prefer the explicit error for cases where it isn't, allowing you to catch such exceptions explicitly.

Practical Example:

````python
text = "ChatGPT is helpful"

# Using find()
position = text.find("helpful")
if position != -1:
    print(f"'helpful' found at index {position}")
else:
    print("'helpful' not found")

# Using index()
try:
    position = text.index("helpful")
    print(f"'helpful' found at index {position}")
except ValueError:
    print("'helpful' not found")
````

### Performance of index( ) and find( )

#### Memory Complexity:

- **Memory Complexity (Space complexity)**:
  - Both methods operate in **O(1)** memory complexity (constant space).
  - They don't require extra memory allocations proportional to input size, as they perform searches directly on the original string.

#### Time Complexity:

- **Time Complexity** for both methods is **O(n \* m)**:
  - **n**: length of the string being searched.
  - **m**: length of the substring you're searching for.

However, practically speaking:

- **Best Case**: If the substring matches immediately (at the beginning), it's O(m).
- **Worst Case**: If the substring is near the end or absent entirely, it's O(n * m).

> [!note]
>
> Practical Considerations:
>
> - **Both methods internally use a straightforward linear search** algorithm.
> - Since strings in Python are immutable, neither method modifies the original string, making memory overhead minimal.
> - No significant performance difference between `find()` and `index()`. Their internal mechanisms are nearly identical.
>
> **Performance**: Virtually identical. Choose based on the desired error-handling behavior:
>
> - `find()` is slightly easier if you expect frequent missing substrings (no exception handling overhead).
> - `index()` is clearer for catching unexpected behavior explicitly.

---

## String Alignment and Padding

**string alignment and padding** are common operations used to format strings by controlling their layout and presentation.

> [!note]
>
> Python provides three built-in methods to align and pad strings:
>
> **Padding**: Adds characters to fill extra spaces to reach a desired width.
>
> **Alignment**: Determines where the original text is positioned relative to the padding.
>
> - **`str.ljust(width[, fillchar])`** — Left alignment
> - **`str.rjust(width[, fillchar])`** — Right alignment
> - **`str.center(width[, fillchar])`** — Center alignment

```python
text = "Python"

# Left-align with spaces (default)
print(text.ljust(10))        # "Python    "

# Right-align with spaces (default)
print(text.rjust(10))        # "    Python"

# Center-align with spaces (default)
print(text.center(10))       # "  Python  "

# Custom padding character ('-')
print(text.center(10, '-'))  # "--Python--"
```

---

![Screenshot 2025-04-01 at 10.42.23 PM](/Users/patrickedwardtapayan/Library/Application Support/typora-user-images/Screenshot 2025-04-01 at 10.42.23 PM.png)

```python
print(f"{'Name':<15}{'Age':^10}{'City':>15}")
print("-" * 40)
print(f"{'Alice':<15}{25:^10}{'New York':>15}")
print(f"{'Bob':<15}{30:^10}{'Los Angeles':>15}")

Name               Age             City
----------------------------------------
Alice               25         New York
Bob                 30      Los Angeles

```

---

## Strip( ), rstrip( ), strip( )

In Python, **`strip()`**, **`rstrip()`**, and **`lstrip()`** are string methods used to remove unwanted leading or trailing characters (such as spaces, newlines, tabs, or custom characters) from strings.

### `strip()` Method:

- Removes characters from **both ends** (left and right) of a string.
- Default behavior removes whitespace (`space`, `tab`, `newline`) from both sides.
- You can also specify characters to remove.

```python
# syntax
str.strip([chars])

text = "   Python   "
print(text.strip())  # "Python"

text = "---Python---"
print(text.strip("-"))  # "Python"

text = "\n\tPython\n"
print(text.strip())  # "Python"
```

### `rstrip()` and `lstrip( )` Method:

`rstrip( )`:

- Removes characters from the **right end** (trailing side) of a string.
- Default behavior removes whitespace from the right side.
- You can specify custom characters.

```python
#syntax
str.rstrip([chars])

text = "Python     "
print(text.rstrip())  # "Python"

text = "Python---"
print(text.rstrip("-"))  # "Python"

text = "Python\n\t"
print(text.rstrip())  # "Python"

```

- Removes characters from the **left end** (leading side) of a string.
- Default behavior removes whitespace from the left side.
- You can specify custom characters.

`lstrip( )`:

- Removes characters from the **left end** (leading side) of a string.

- Default behavior removes whitespace from the left side.

- You can specify custom characters.

```python
#syntax
str.lstrip([chars])

text = "     Python"
print(text.lstrip())  # "Python"

text = "---Python"
print(text.lstrip("-"))  # "Python"

text = "\t\nPython"
print(text.lstrip())  # "Python"

```

> [!important]
>
> **Important Note**:
>
> - These methods **DO NOT** modify the original string, as strings are immutable.
> - They return a **new** modified string instead.
>
> **common usecases:**
>
> - Cleaning user input (e.g., removing accidental spaces).
>
> - Pre-processing strings before parsing or comparing.
>
> - Reading from files and cleaning lines (`.strip()` is very common when reading lines from text files).

---

## `split( )` , `join( )`, `replace()` methods

> [!important]
>
> `split()`  returns a list of strings.
>
> `join()` works **only** with iterables containing **strings**. To join numbers or other types, convert them first to strings.

Example 1: Extracting words from a sentence 

```python
sentence = "Hello there, how are you?"
words = sentence.split()
print(words)
# Output: ['Hello', 'there,', 'how', 'are', 'you?']
```

Example 2: CSV to list and back to CSV String

```python
csv_data = "red,green,blue,yellow"
colors = csv_data.split(',')
print(colors)  # ['red', 'green', 'blue', 'yellow']

new_csv = '|'.join(colors)
print(new_csv)  # "red|green|blue|yellow"
```

### split( ) method:

The `split()` <u>**method splits a string into a list.**</u> By default, it splits on **whitespace** (spaces, tabs, newlines), but you can specify a custom separator.

example:

```python
str.split(sep=None, maxsplit=-1)
```

`sep`: (optional) Separator to split by. Defaults to whitespace.

`maxsplit`: (optional) Limits the number of splits. Default is unlimited.

Examples:

- Split by whitespace (default):

```python
text = "Python is awesome"
print(text.split())  # ['Python', 'is', 'awesome']
```

- Split by custom separator:

```python
text = "apple,banana,cherry"
print(text.split(","))  # ['apple', 'banana', 'cherry']
```

- using `maxsplit`:

```python
text = "one two three four"
print(text.split(" ", maxsplit=2))  
# Output: ['one', 'two', 'three four']
```

## join( ) Method

The `join()` method combines elements of an iterable (usually a list or tuple) into a single string, inserting a separator between each element.

```python
separator.join(iterable)
```

- The separator is the string placed between each element.

- The iterable contains strings (or elements convertible to strings).

Examples:

- Join with space:

```python
words = ['Python', 'is', 'awesome']
sentence = ' '.join(words)
print(sentence)  # "Python is awesome"
```

- Join with comma:

```python
fruits = ['apple', 'banana', 'cherry']
fruit_str = ','.join(fruits)
print(fruit_str)  # "apple,banana,cherry"
```

- Join with newline (`'\n'`):

```python
lines = ['Line 1', 'Line 2', 'Line 3']
text = '\n'.join(lines)
print(text)

#output:
Line 1
Line 2
Line 3
```

---

## Prefix and Suffix Methods

> [!important]
>
> 📌 **Important Notes**:
>
> - Both methods are **case-sensitive**:
>
> ```python
> text = "Python"
> print(text.startswith("python"))  # False
> ```
>
> - They do not alter the original string

### startswith( ) method:

Checks if the string **starts** with the specified substring (prefix). returns a `bool` value

```python
#sytnax:
str.startswith(prefix[, start[, end]])
```

`prefix`: A string (or tuple of strings) you want to check at the start of the string.

`start` (optional): Index position to start checking from.

`end` (optional): Index position to end checking.

Example:

- simple use

```python
text = "Hello World"
print(text.startswith("Hello"))  # True
print(text.startswith("World"))  # False
```

- using tuple of prefixes

```python
text = "python_script.py"
print(text.startswith(("python", "java")))  # True
```

- Using `start` and `end` parameters:

```python
text = "Hello World"
print(text.startswith("World", 6))  # True
```

### endswith( ) method:

Checks if the string **ends** with the specified substring (suffix).

```python
#syntax
str.endswith(suffix[, start[, end]])
```

`suffix`: A string (or tuple of strings) you want to check at the end of the string.

`start` (optional): Starting index to begin checking from.

`end` (optional): Index to stop checking at.

```python
text = "report.pdf"
print(text.endswith(".pdf"))  # True
print(text.endswith(".txt"))  # False


# Using tuple of suffixes:
filename = "image.png"
print(filename.endswith((".png", ".jpg", ".gif")))  # True

# Using start and end parameters:
text = "Hello World"
print(text.endswith("Hello", 0, 5))  # True (checking "Hello")
```


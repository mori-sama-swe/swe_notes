# Formatted Printing

## ASCII

> [!important]
>
> ASCII stands for American Standard Code for Information Interchange. **It’s a character encoding standard that assigns unique numerical values to letters, digits, punctuation marks, and some control characters.**

Example:
```python
'A' is 65
'a' is 97
'!' is 33
```

ASCII uses 7 bits, which means it can represent 128 different characters (from 0 to 127)

> [!important]
>
> In ASCII, **65 is indeed the start of the uppercase alphabet**, where it corresponds to the letter **'A'**. The uppercase letters range from **65 ('A')** to **90 ('Z')**. However, if you're asking about the *entire alphabet*, including lowercase letters, those begin at **97 ('a')** and go up to **122 ('z')**.
>
> So, to clarify:
>
> - **Yes**, 65 is the start of the uppercase alphabet.
> - **No**, it’s not the start of the lowercase alphabet, which begins at 97.
>
> It depends on whether you meant just the uppercase letters or the full alphabet including both cases!

---

### How to Read ASCII in Python

Python makes it easy to work with ASCII codes using two built-in functions: `ord()` and `chr().`  with these functions, you can "read" ASCII by converting between characters and their numerical codes whenever you need to.

### Why It Matters

Understanding ASCII helps you:

- **Manipulate text**: Convert characters to numbers for tasks like encryption or data processing.
- **Compare characters**: Sort strings or check if a character is a letter (e.g., ASCII values 65-90 are uppercase letters, 97-122 are lowercase).
- **Work with data**: ASCII is used in file formats, network protocols, and more.

### `ord()`: character to ASCII Value

The `ord()` function takes a single character and returns its ASCII (or Unicode) value. Here are some examples:

```python
print(ord('A'))  # Output: 65
print(ord('a'))  # Output: 97
print(ord('!'))  # Output: 33
```

### `chr()`: ASCII Value to Character

The `chr()` function does the opposite—it takes an ASCII (or Unicode) value and returns the corresponding character:

```python
print(chr(65))  # Output: 'A'
print(chr(97))  # Output: 'a'
print(chr(33))  # Output: '!'
```

---

Examples Working With Strings:
Let’s say you have the string "ABC". You can convert it to a list of ASCII values and back like this:

```python
# Convert string to ASCII values
ascii_values = [ord(char) for char in "ABC"]
print(ascii_values)  # Output: [65, 66, 67]

# Convert ASCII values back to string
original_string = ''.join(chr(num) for num in [65, 66, 67])
print(original_string)  # Output: 'ABC'
```

---

## Escape Sequence

> [!important]
>
> In Python, escape sequences are special character combinations used within strings to represent characters that are difficult or impossible to type directly. 
>
> They consist of a `backslash (\)` followed by one or more characters, which together tell Python to interpret them in a specific way.
>
> For example, instead of typing an actual newline (which you can’t do in a string), you use \n to represent it. Escape sequences allow you to format text, include special characters, or control how output behaves.

`\f`: Form feed – Advances to the next "page" (rarely used in modern contexts).

```python
print("Page1\fPage2")
# Output: Page1
#         Page2 (effect varies by system)
```

---

`\"`: Double quote – Allows a double quote inside a string enclosed by double quotes.

```python
print("She said, \"Hello!\"")
# Output: She said, "Hello!"
```

---

`\'`: Single quote – Allows a single quote inside a string enclosed by single quotes.

```python
print('It\'s a sunny day')
# Output: It's a sunny day
```

`\\:` Backslash – Represents a single backslash

```python
print("This is a backslash: \\")
# Output: This is a backslash: \
```

---

### How Are Escape Sequences Used in Python?

Escape sequences are used within string literals (text enclosed in quotes) to achieve the following:

> [!note]
>
> - **Escape sequences** in Python are special codes starting with a backslash (\) that represent hard-to-type or special characters in strings.
> - They’re used for **formatting text** (e.g., \n, \t), **adding special characters** (e.g., \', \", \\), and occasionally **controlling output** (e.g., \r, \b).
> - **Raw strings** (r"...") treat backslashes literally, ignoring escape sequences.
> - **Unicode escape sequences** (\uXXXX) let you include a vast range of characters.
>
> Escape sequences are essential for working with strings in Python, giving you precise control over text display and manipulation.

Text Formatting: They add structure to output, like new lines (\n) or tabs (\t), making it more readable.

```python
print("Name:\tAlice\nAge:\t30")
# Output:
# Name:   Alice
# Age:    30
```

Including Special Characters: They let you include characters that Python might otherwise misinterpret (like quotes) or that can’t be typed (like backslashes).

```python
print("Path: C:\\Users\\Name")
# Output: Path: C:\Users\Name
```

---


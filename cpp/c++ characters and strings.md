# Characters and Strings in C++



In C++, **characters** and **strings** are essential data types for handling text. They serve different purposes: ***<u>characters represent single symbols, while strings represent sequences of characters.</u>*** 

## Characters In C++

A **character** is a *<u>single symbol, like a letter, digit, or punctuation mark. In C++, characters are represented using the char data type (and related types).</u>*

> [!NOTE]
>
> **Key Details:**
>
> - **Type**: char (1 byte, typically 8 bits).
> - **Range**:
>   - Signed: -128 to 127.
>   - Unsigned: 0 to 255 (used for extended ASCII).
> - **Purpose**: Stores a single character, often from the ASCII table (e.g., 'A' is 65, 'a' is 97).
> - **Literal Syntax**: Enclosed in single quotes (e.g., 'A', '5', '!').

```cpp
char letter = 'A';     // Stores the character 'A' (ASCII value 65)
char digit = '7';      // Stores '7' (ASCII value 55)
char newline = '\n';   // Escape sequence for a new line
```

### `Char` Variants:

- **signed char**: Explicitly signed (rarely used for text).

- **unsigned char**: For raw bytes or extended character sets.

- **wchar_t**: Wide character (2 or 4 bytes) for larger character sets like Unicode.

### Operations with Characters

Characters can be treated as integers because they’re stored as numeric values (ASCII codes).

```cpp
char c = 'A';
c = c + 1; // c becomes 'B' (66)
std::cout << c; // Outputs: B
```

---

## Strings in C++

A **string** is a sequence of characters. C++ handles strings in two primary ways: **C-style strings** (from C) and **C++ std::string** (modern, preferred).

> [!NOTE]
>
> Key Points to Understand:
>
> - **Characters**: Building blocks of text. Think of them as single units (e.g., 'a', '5').
> - **C-Style Strings**: Arrays of characters with a \0 terminator. Low-level, inherited from C.
> - **std::string**: Modern, flexible, and safer. Use this unless you need C compatibility.
> - **Memory**: Characters are fixed-size (1 byte for char), while strings vary based on content.

### C-Style Strings

**c-style strings:** A sequence of characters in memory with a `\0` at the end to mark its end.

```cpp
char str[] = "world";
std::cout << strlen(str); // Outputs: 5 (excludes \0
```

> [!NOTE]
>
> Key Points:
>
> - Size includes the null terminator (e.g., "hello" takes 6 bytes: 5 letters + \0).
> - **Manual management:** You must ensure enough space and proper termination.
>   - manual management of allocating and deallocating memory
> - Used with C library functions (e.g., strlen, strcpy from <cstring>).

Example:

```cpp
char greeting[] = "hello"; // Array: {'h', 'e', 'l', 'l', 'o', '\0'}
char fixed[6] = {'h', 'i', '\0', 'x', 'y', 'z'}; // "hi" (ignores after \0)
```

##### Declaring and Intializing C++ Strings

```cpp
char str1[] = "Hello";  // Implicitly adds '\0'
char str2[6] = "Hello"; // Explicit size including '\0'
char str3[] = {'H', 'e', 'l', 'l', 'o', '\0'}; // Manual definition
```

```cpp
#include <iostream>
#include <cstring>

int main(){
	char my_name[8];
	my_name = "Pat"; // ERROR  - compile error because you can't re-assign an array - you can modify its invidviual contents but not the array name
	strcpy(my_name,"Pat"); // OK 

}
```

### C++ `std::strings`


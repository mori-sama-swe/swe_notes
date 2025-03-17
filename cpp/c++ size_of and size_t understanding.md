
# size_of and size_t understanding

## Understanding `size_t`

In C++, `size_t` is an unsigned integer type defined in the standard library. **It is commonly used to represent the size of objects in memory, such as the number of elements in an array or the size of a data structure.** 

> [!Important]
>
> **The exact size of size_t depends on the system architecture (e.g., 32-bit or 64-bit),**

 but it is designed to be large enough to hold the maximum size of any object or memory block that the system can support.

> [!NOTE]
>
> **Key Characteristics **
>
> - **Unsigned**: It cannot represent negative values, so its range starts at 0 and goes up to a maximum value determined by its bit width.
> - **Platform-Dependent Size**
> - **Purpose**: It is the type returned by the sizeof operator and is used in functions like strlen(), std::vector::size(), and other standard library functions that deal with sizes or counts.


### why use `size_t`

- Being unsigned, it avoids issues with negative values when dealing with sizes or counts, which are inherently non-negative.

- > [!IMPORTANT]
  >
  > in short, **size_t** is a versatile, unsigned integer type tailored for representing sizes and counts in a way that is safe and efficient for the given system.

- > [!IMPORTANT]
  >
  > It ensures portability across different platforms since its size adapts to the system's architecture.

**Example Usage:**

```cpp
#include <iostream>
#include <vector>

int main() {
    // size_t as return type of sizeof
    size_t size = sizeof(int);
    std::cout << "Size of int: " << size << " bytes" << std::endl;

    // size_t with std::vector
    std::vector<int> vec = {1, 2, 3, 4, 5};
    size_t vecSize = vec.size();
    std::cout << "Vector size: " << vecSize << std::endl;

    return 0;
```

---

## Understanding `size_of()`

In C++, **sizeof** is a unary operator that **<u>returns the size, in bytes, of a type or an object in memory.</u>** It’s a compile-time tool, meaning it computes sizes during compilation rather than at runtime, making it both efficient and critical for memory-related tasks.

> [!NOTE]
>
> **Purpose**: Determines the amount of memory (in bytes) allocated for a type, variable, or expression.
>
> **Return Type**: std::size_t, an unsigned integer type defined in <cstddef> (typically unsigned long or unsigned long long depending on the platform).
>
> **Compile-Time**: Evaluated by the compiler, not during execution.

Syntax:

```cpp
sizeof(type) (e.g., sizeof(int)).
sizeof expression or sizeof(variable) (e.g., sizeof(x)).
```

Basic Example:

```cpp
#include <iostream>
int main() {
    int x = 42;
    std::cout << sizeof(int) << "\n";  // Size of int type (e.g., 4 on many systems)
    std::cout << sizeof(x) << "\n";    // Size of variable x (same as int, e.g., 4)
    return 0;
}
```

### how `sizeof` works

> [!IMPORTANT]
>
> The size returned by sizeof depends on:
>
> 1. **Data Type**: Each type has a predefined or calculated size.
> 2. **Platform**: Sizes vary across architectures (e.g., 32-bit vs. 64-bit systems).
> 3. **Compiler Implementation**: Padding, alignment, and type definitions can differ.

example:

```cpp
std::cout << sizeof(char) << "\n";    // 1
std::cout << sizeof(int) << "\n";     // 4 (typically)
std::cout << sizeof(double) << "\n";  // 8
std::cout << sizeof(int*) << "\n";    // 8 (on 64-bit)
```

> [!NOTE]
>
> Practical Uses:
>
> **Array Length Calculation**:
>
> ```cpp
> int arr[10];
> size_t len = sizeof(arr) / sizeof(arr[0]); // 10
> ```
>
> **Memory Allocation**:
>
> ```cpp
> int* ptr = (int*)malloc(sizeof(int) * 5); // 20 bytes for 5 ints
> ```
>
> **Debugging/Portability**:
>
> ```cpp
> std::cout << sizeof(long) << "\n"; // 4 or 8?
> ```

### `sizeof` relationship with arrays

For a statically declared **array**, *<u>**sizeof gives the total size of the array (elements × element size).**</u>*

- For a **pointer** to an array (e.g., function parameter), <u>***it gives the pointer size, not the array size.***</u>

```cpp
int arr[5] = {1, 2, 3, 4, 5};
std::cout << sizeof(arr) << "\n";      // 20 (5 ints × 4 bytes each)
std::cout << sizeof(arr[0]) << "\n";   // 4 (size of one int)
std::cout << sizeof(arr) / sizeof(arr[0]) << "\n"; // 5 (number of elements)

int* ptr = arr;
std::cout << sizeof(ptr) << "\n";      // 8 (size of pointer, not array)
```

### `sizeOf` relationship with structures and classes

`sizeof` for a struct or class includes all members, plus **padding** for alignment.

- **Alignment**: Compilers add extra bytes to ensure members align with memory boundaries (e.g., 4-byte or 8-byte alignment on many systems).

```cpp
struct Example {
    char c;    // 1 byte
    int i;     // 4 bytes
};
std::cout << sizeof(Example) << "\n"; // 8 (not 5, due to padding)
```

**Why 8?**: The char (1 byte) is followed by 3 padding bytes to align int on a 4-byte boundary, totaling 8 bytes.


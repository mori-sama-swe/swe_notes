# Dynamic Memory Allocation

**dynamic memory allocation** allows you to allocate memory at runtime rather than compile-time, giving your program flexibility to manage memory based on its needs. 

This is in contrast to **static** or **automatic** allocation (e.g., stack variables), where memory size is fixed at compile-time or scoped to a function. Dynamic memory is allocated on the **heap**, and **<u>C++ provides tools like *new*, *delete*, and standard library containers to handle it.</u>**

> [!TIP]
>
> **Heap Allocation**: Use `new` for single objects, `new[]` for arrays.
>
> **Deallocation**: Match `new` with `delete`, new[] with delete[].
>
> **Lifetime**: You control when memory is freed (unlike stack variables).
>
> **Modern Practice**: Prefer std::unique_ptr, std::shared_ptr, or containers over raw pointers.

---

### what is dynamic memory allocation?

> [!NOTE]
>
> **Definition**: Allocating memory during program execution, typically on the heap, with sizes determined at runtime.
>
> **Why Use It?**:
>
> - When the amount of memory needed isn’t known until runtime (e.g., user input, file sizes).
> - For objects that need to persist beyond their declaring scope.
> - To manage large or resizable data structures.
>
> **Key Tools**: new, delete (C++ operators), and C-style malloc/free (less common in modern C++).

## `new` operator

> [!IMPORTANT]
>
> **Purpose**: *<u>Allocates memory on the heap and returns a pointer to it.</u>*

syntax:

```cpp
type* ptr = new type;// For a single object
type* ptr = new type[size]; // For an array
```

```cpp
// SINGLE OBJECT
int* ptr = new int;     // Allocates memory for one int
*ptr = 42;              // Assigns value
std::cout << *ptr;      // Outputs: 42

// WITH INITIALIZATION
int* ptr = new int(10); // Allocates and initializes to 10

// ARRAY
int* arr = new int[5];  // Allocates memory for 5 ints
arr[0] = 1; arr[1] = 2; // Assign values
```

## `delete` operator

> [!IMPORTANT]
>
> **Purpose**: Deallocates memory previously allocated with new, freeing it back to the heap.
>
> - **Mismatch Error**: Using delete on an array or delete[] on a single object is undefined behavior.
>
> - **Null Pointer**: Safe to delete a nullptr (no-op).
>
>   - ```cpp
>     int* ptr = nullptr;
>     delete ptr; // OK, does nothing
>     ```

```cpp
delete ptr; //For a single object:
delete[] ptr; // For an array:
```

---

## Allocating Memory Via Heap or Stack

> [!NOTE]
>
> **Stack**: Automatic memory (e.g., int x;). Fast, but size is fixed and lifetime is scoped.
>
> **Heap**: Dynamic memory (e.g., new int;). Slower, but flexible size and lifetime controlled manually.
>
> - use `new` for single objects, use `new[]` for arrays

```cpp
void stackExample() {
    int x = 5; // Stack, destroyed when function ends
}
void heapExample() {
    int* ptr = new int(5); // Heap, persists until deleted
    // Must delete ptr manually
}
```

> [!WARNING]
>
> Common Pitfalls:
>
> **Memory Leaks**: Forgetting to delete heap memory.
>
> ```cpp
> int* ptr = new int(10);
> // No delete: memory leak!
> ```
>
> **Double Deletion**: Deleting the same pointer twice is undefined behavior.
>
> ```cpp
> int* ptr = new int;
> delete ptr;
> delete ptr; // Crash or undefined
> ```
>
> - Fix: Set to nullptr after deletion.
>
> ```cpp
> delete ptr;
> ptr = nullptr; // Safe
> ```
>
> **Dangling Pointers**: Accessing memory after it’s freed.
>
> ```cpp
> int* ptr = new int(5);
> delete ptr;
> std::cout << *ptr; // Undefined behavior
> ```

---

## Working With Objects

For **<u>classes</u>**, **new** calls the **constructor**, and **delete** calls the **destructor**.

example:

```cpp
#include <iostream>
class MyClass {
public:
    MyClass() { std::cout << "Constructor\n"; }
    ~MyClass() { std::cout << "Destructor\n"; }
};
int main() {
    MyClass* obj = new MyClass; // Outputs: Constructor
    delete obj;                 // Outputs: Destructor
    return 0;
}
```

Array of Objects:

```cpp
MyClass* arr = new MyClass[2]; // Calls default constructor twice
delete[] arr;                 // Calls destructor for each object
```

---

## C-Style Allocation

**malloc**: Allocates raw memory (no constructor).

```cpp
int* ptr = (int*)malloc(sizeof(int) * 3); // 12 bytes
```

**free**: Deallocates it (no destructor).

```cpp
free(ptr);
```

> [!TIP]
>
> **Why Avoid**: No type safety, no constructor/destructor calls. Use new/delete instead.

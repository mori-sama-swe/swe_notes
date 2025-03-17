# Understanding Functions in C++

## Functions

## What is a Function?

> [!NOTE]
>
> **functions** are reusable blocks of code that perform specific tasks. They allow you to organize your program into modular, manageable pieces, improving readability, reusability, and maintainability. **Functions** can take inputs <u>**parameters**</u>, process them, and **<u>return an output (or perform actions without returning anything).</u>** 

> [!NOTE]
>
> **Components of a Function:**
>
> - Return type (what it gives back).
>
> - Name (how you call it).
>
> - Parameters (inputs it accepts, optional).
>
> - Body (the code it executes).

Basic Syntax:

```cpp
return_type function_name(parameter_list) {
    // Function body: statements
    return value; // Optional, based on return_type
}
```

Example:

```cpp
int add(int a, int b) { // Returns an int, takes two ints
    return a + b;       // Returns the sum
}

int main() {
    int sum = add(3, 4); // Calls add, sum = 7
    std::cout << sum;    // Outputs: 7
    return 0;
}
```

---

### Key Elements of a Function

#### `return` statement

the `return` statement:

- **<u>*Used inside the function body to send a value back to the caller.*</u>**
- Must match the declared return type (or be implicitly convertible to it).
- Example: return 5; in a function with int return type.

`return type` : *<u>**specifies what the function returns (e.g., int, double, void).**</u>*

example of a return statement:

```cpp
#include <iostream>
#include <string>

void sayHi() {
    std::cout << "Hi!\n";
}

int add(int a, int b) {
    return a + b;
}

std::string greet(std::string name) {
    return "Hello, " + name;
}

int& modify(int* arr) {
    return arr[0]; // Returns reference to first element
}

int main() {
    sayHi();                       // Void: no return
    std::cout << add(3, 4) << "\n"; // Returns 7
    std::cout << greet("Bob") << "\n"; // Returns "Hello, Bob"
    
    int arr[2] = {10, 20};
    modify(arr) = 50;              // Modifies arr[0] via reference
    std::cout << arr[0] << "\n";   // Prints 50
    return 0;
}
```

- Can be any type: primitives, pointers, objects, etc.

  - > [!NOTE]
    >
    > ###### **Void**: Use it for functions that don’t need to return anything—just do the job and exit.
    >
    > **Auto**: A powerful tool for letting the compiler handle return type deduction, especially useful for complex or generic code. Pair it with trailing return types when needed.
    >
    > - **`void`** return type means the function does **not return any value** to the caller. It’s essentially a way to say, “This function does its job and stops there—no result needed.”
    >   - **Used when the function’s purpose is to change something** (e.g., a parameter passed by reference) rather than compute a value.
    >   - You can use return; to bail out early if a condition is met.
    >
    > ```cpp
    > void functionName(parameters) {
    >     // Do something
    > }
    > ```
    >
    > - **`auto`**: The auto keyword, introduced in C++11, lets the compiler **automatically deduce the return type** of a function based on the value returned in the return statement. It’s a way to say, “I’ll let the compiler figure out what this function returns.”
    >
    > ```cpp
    > auto functionName(parameters) {
    >     return some_value; // Compiler deduces type from this
    > }
    > ```
    >
    > ```cpp
    > #include <iostream>
    > #include <vector>
    > 
    > auto getMax(int a, int b) {
    >     return (a > b) ? a : b; // Deduced as int
    > }
    > 
    > auto getSize(const std::vector<int>& v) -> size_t {
    >     return v.size(); // Explicitly size_t
    > }
    > 
    > int main() {
    >     std::cout << getMax(5, 10) << "\n"; // 10
    >     std::vector<int> vec = {1, 2, 3};
    >     std::cout << getSize(vec) << "\n";  // 3
    >     return 0;
    > }
    > ```


> [!WARNING]
>
> **Mismatched Return Type**:
>
> - **<u>The value returned must match the declared return type,</u>** or the compiler will throw an error.
> - Example: Declaring int foo() but returning 3.14 (a double) causes a compilation error unless explicitly cast.
>
> **Returning Local Variables by Reference**:
>
> - <u>**Returning a reference or pointer to a local variable (which is destroyed when the function exits)**</u> causes dangling references/pointers.
> - Example:
>   - Fix: Return by value or use static/dynamic memory.
>
> ```cpp
> int& danger() {
>     int x = 5;
>     return x; // x is destroyed after return
> }
> ```
>
> **Performance with Large Objects**:
>
> - Returning large objects by value can be expensive due to copying.
> - Use move semantics (C++11) or references/pointers to optimize.
>
> ```cpp
> std::vector<int> getData() {
>     std::vector<int> v = {1, 2, 3};
>     return v; // Move semantics avoid copying
> }
> ```

---

#### Parameters

Pre-Reqs: [Understanding Pointers](../cpp/c++ pointers and pointer arithmetic.md)

In C++, **parameters** are <u>***variables defined in a function’s declaration that allow you to pass data into the function when it’s called. They act as placeholders for the values (arguments) provided by the caller.***</u> How parameters are handled—especially how **<u>*they’re passed (by value, by reference, or otherwise)*</u>**—is a key concept in C++ that affects both functionality and performance. 

> [!NOTE]
>
> **Definition**: Parameters are the variables listed in a function’s parentheses in its declaration or definition.
>
> - **Arguments**: **The actual values passed to the function** when it’s called (e.g., add(3, 4) passes 3 and 4 as arguments to a and b).

syntax and example:
```cpp
return_type function_name(parameter_type parameter_name, ...) { ... }
```

```cpp
int add(int a, int b) { // a and b are parameters
    return a + b;
}
```

> [!NOTE]
>
> How Parameters Are Used:
>
> 1. **Input to Functions**
>    - Parameters let functions operate on external data without hardcoding values.
>    - Example: void print(int x) { std::cout << x; } prints whatever integer is passed.
> 2. **Control Behavior**
>    - Parameters can dictate what a function does.
>    - Example: void repeat(int times) { for (int i = 0; i < times; i++) std::cout << "Hi\n"; }
> 3. Return Calculations
>    - Used to compute and return a result.
>    - Example: double average(double x, double y) { return (x + y) / 2; }
> 4. **Modify External Data**
>    - When passed by reference or pointer, parameters can change the caller’s data.
>    - Example: void swap(int& a, int& b) { int temp = a; a = b; b = temp; }

##### Passing by Value vs Passing By Reference

C++ offers multiple ways to pass parameters, with **pass-by-value** and **pass-by-reference** being the most common. Each has distinct mechanics, use cases, and implications.

> [!IMPORTANT]
>
> **Pass-by-value**:  A copy of the argument is made and passed to the function. The original data remains unchanged.
>
> **Pass-by-reference**: The function gets a reference to the original argument, not a copy. Changes to the parameter affect the caller’s data.

Practical Example:

```cpp
#include <iostream>
#include <string>

// Pass-by-value (copy)
void byValue(int x) {
    x += 10;
    std::cout << "Inside byValue: " << x << "\n";
}

// Pass-by-reference (modifies original)
void byReference(int& x) {
    x += 10;
    std::cout << "Inside byReference: " << x << "\n";
}

// Pass-by-const-reference (no copy, no modify)
void print(const std::string& s) {
    std::cout << "String: " << s << "\n";
}

// Pass-by-pointer (optional modification)
void byPointer(int* x) {
    if (x) *x += 10;
}

int main() {
    int a = 5;
    byValue(a);         // a unchanged (5)
    std::cout << "After byValue: " << a << "\n";

    byReference(a);     // a becomes 15
    std::cout << "After byReference: " << a << "\n";

    std::string s = "Hello";
    print(s);           // No copy, just prints

    byPointer(&a);      // a becomes 25
    std::cout << "After byPointer: " << a << "\n";

    return 0;
}

Inside byValue: 15
After byValue: 5
Inside byReference: 15
After byReference: 15
String: Hello
After byPointer: 25
```

> [!NOTE]
>
> ### Summary
>
> - **Parameters** bring flexibility to functions by accepting input.
> - **Pass-by-Value**: Copies data, safe but potentially slow.
> - **Pass-by-Reference**: Uses original data, efficient but requires caution.
> - **Other Options**: Pointers for explicit control, const references for efficiency + safety, move semantics for modern optimization.

##### Pass-by-Value

**Use Case**: When you just need the value and don’t intend to modify the original data.

**Syntax**: `type parameter_name` (no special symbols).

```cpp
void increment(int x) {
    x++; // Modifies the copy, not the original
}

int main() {
    int a = 5;
    increment(a);
    std::cout << a << "\n"; // Still 5
    return 0;
}
```

##### Pass-by-Reference

> [!IMPORTANT]
>
> **Definition**: When a **parameter is passed by reference**, the function receives an alias (or reference) to the original argument rather than a copy. Any changes to the parameter inside the function directly affect the original data.

**Syntax**: `type& parameter_name` (uses the **&** symbol).

example:

- Here, x is a reference to `a`. Changing `x` changes a because they’re the same object in memory.

```cpp
void increment(int& x) {
    x++; // Modifies the original
}

int main() {
    int a = 5;
    increment(a);
    std::cout << a << "\n"; // Now 6
    return 0;
}
```

> [!NOTE]
>
> **How Pass-by-Reference Works Under the Hood**
>
> - **Memory Perspective**: A reference isn’t a separate entity with its own memory; it’s just another name for the original variable. The compiler ensures that operations on the reference operate on the original memory address.
> - **No Overhead**: Unlike pass-by-value (which creates a copy), pass-by-reference passes a lightweight alias—typically implemented as a pointer internally by the compiler, but you don’t deal with pointer syntax.
> - **Contrast with Pointers**: While pass-by-pointer (type*) also accesses the original data, references are syntactically cleaner and don’t require dereferencing (*).

##### Pass-by-Pointer

**How it Works**: A pointer to the argument is passed. **The function can modify the original data via [dereferencing](../cpp/c++ pointers and pointer arithmetic.md#Derefrencing a Pointer)**

- **Use Case**: Legacy code, optional parameters, or when interfacing with C-style APIs.

```cpp
void increment(int* x) {
    (*x)++; // Dereference to modify original
}

int main() {
    int a = 5;
    increment(&a); // Pass address
    std::cout << a << "\n"; // Now 6
    return 0;
}
```

> [!IMPORTANT]
>
> Difference between By Reference vs By Pointer
>
> ```cpp
> void byRef(int& x) { x += 10; }
> void byPtr(int* x) { *x += 10; }
> 
> int main() {
>     int a = 5, b = 5;
>     byRef(a);     // a becomes 15
>     byPtr(&b);    // b becomes 15
>     std::cout << a << " " << b << "\n"; // 15 15
>     return 0;
> }
> ```
>

##### Passing-an-Array

in C++, when you pass an array to a function, it’s **effectively passed by reference**—but not in the way you might think if you’re picturing the & reference syntax. Instead, **the array’s name “decays” into a pointer to its first element**, and **that pointer is passed by value**. 

> [!important]
>
> *This means the function works with the original array’s memory, not a copy, so changes inside the function affect the original array.*
>
> In C++ (and C, where this behavior comes from), arrays aren’t treated as full objects when passed to functions. *<u>**The array name (e.g., myArray) is just a shorthand for the memory address of its first element. When you pass it, you’re really passing a pointer to that starting address. The function gets this pointer, not a duplicate of the whole array, which is why it’s efficient but also why modifications stick.**</u>*

Is It Really “By Reference”?

- **Technically, no**: The pointer itself is passed by value (a copy of the address), but because it points to the original array’s memory, it behaves like a reference to the array’s contents.
- **Practically, yes**: You’re working with the original data, not a copy, so it feels like pass-by-reference.

**Example 1: Passing an Array and Modifying It**

- **What’s happening**: `arr` in the function is a pointer to myArray[0]. Changing arr[0] modifies the original array because it’s the same memory.

```cpp
#include <iostream>

void modifyArray(int arr[], int size) {
    arr[0] = 999;  // Changes the original array
    std::cout << "Inside function: " << arr[0] << std::endl;
}

int main() {
    int myArray[] = {1, 2, 3};
    std::cout << "Before: " << myArray[0] << std::endl;

    modifyArray(myArray, 3);  // Pass the array and its size

    std::cout << "After: " << myArray[0] << std::endl;
    return 0;
}

Output:
Before: 1
Inside function: 999
After: 999
```

**Example 2: Array Decay to Pointer**

-  **Explanation**: myArray decays to a pointer (int*), and arr gets a copy of that pointer. Same address, same data.

```cpp
#include <iostream>

void printAddress(int arr[]) {
    std::cout << "Address in function: " << arr << std::endl;
}

int main() {
    int myArray[] = {10, 20, 30};
    std::cout << "Address in main: " << myArray << std::endl;
    printAddress(myArray);
    return 0;
}

Output:
Address in main: 0x7ffee4c0a4c0
Address in function: 0x7ffee4c0a4c0
```

> [!note]
>
> **Key Points to Understand**
>
> 1. **No Size Info**: When an array decays to a pointer, the function doesn’t know how big it is. That’s why you often pass the size separately (like int size above).
> 2. **Syntax Trick**: Writing int `arr[]` in the parameter list is just sugar—it’s the same as `int* arr`. Both mean “pointer to an int.”
> 3. **Modifications Stick**: Since the function accesses the original memory, any changes affect the caller’s array.
>
> **Can You Pass a Copy Instead?:** 
>
> - **For control**: If you want a copy or a different behavior, use something like std::vector or std::array (a modern C++ wrapper for fixed-size arrays).
> - **If you don’t want the original array modified, you’d need to manually copy it first (e.g., into a std::vector or another array) and pass that copy.** Arrays themselves don’t get copied automatically—passing the whole thing by value isn’t a thing in C++.

---

### Function ProtoTypes

In C++, a **function prototype** is like a **<u>heads-up to the compiler about a function before you actually define how it works.</u>** It tells the compiler three key things:

- **Return type**: What kind of value the function will give back (e.g., int, double, void if nothing).

- **Function name**: What you’ll call it.

- **Parameters**: What inputs it takes, including their types (e.g., int x, double y).

> [!IMPORTANT]
>
> **Why Use Them?**
>
> - **Order Matters**: In C++, if you call a function before defining it, the compiler won’t know what it is without a prototype. Prototypes let you use functions anywhere in your code.
> - **Error Checking**: They help the compiler catch mistakes, like passing a string when the function expects a number.
> - **Organization**: They’re often put in header files (.h) so multiple parts of a program can use the same functions without repeating code.

syntax and example:

```cpp
return_type function_name(parameter_type parameter_name, ...);
```

```cpp
#include <iostream>

// Prototype at the top
int add(int a, int b);

int main() {
    int sum = add(3, 5);  // Call works because prototype exists
    std::cout << "Sum: " << sum << std::endl;  // Outputs: Sum: 8
    return 0;
}

// Definition later
int add(int a, int b) {
    return a + b;
}
```

> [!tip]
>
> - Prototypes must match their definitions exactly (return type, parameter types, etc.), or you’ll get errors.
> - If a function is defined *before* it’s used (e.g., above main()), you don’t need a separate prototype—the definition acts as one.
> - In big projects, stick prototypes in header files to keep things tidy.

### Function Overloading

> [!NOTE]
>
> Function overloading in C++ is a feature that lets you define multiple functions with the **same name** but **different parameter lists**. **This means you can use the same function name for different tasks, and the compiler figures out which version to call <u>based on the arguments you provide**.</u> It’s a way to make your code more intuitive and flexible.

**How Does It Work?**:

The compiler distinguishes overloaded functions by looking at:

- **Number of parameters**: How many arguments the function takes.
- **Types of parameters**: What data types the arguments are (e.g., int, double, string).
- **Order of parameters**: The sequence of parameter types.

The **return type** alone doesn’t matter for overloading—only the parameter list (also called the function signature) decides which function gets called.

> [!IMPORTANT]
>
> **Rules for Overloading**
>
> 1. Functions must have the **same name**.
> 2. They must differ in at least one of these:
>    - Number of parameters.
>    - Type of parameters.
>    - Order of parameters.
> 3. Return types can be different, but that’s not enough by itself to overload—parameters must differ too.

Example of function overloading with different parameters:

```cpp
#include <iostream>

void print(int x) {
    std::cout << "Integer: " << x << std::endl;
}

void print(int x, int y) {
    std::cout << "Two integers: " << x << " and " << y << std::endl;
}

int main() {
    print(5);        // Calls first version
    print(5, 10);    // Calls second version
    return 0;
}
```

Example of functiion overloading with different types:

```cpp
#include <iostream>

void display(int num) {
    std::cout << "Number: " << num << std::endl;
}

void display(double num) {
    std::cout << "Decimal: " << num << std::endl;
}

void display(const std::string& text) {
    std::cout << "Text: " << text << std::endl;
}

int main() {
    display(42);         // Calls int version
    display(3.14);       // Calls double version
    display("Hello");    // Calls string version
    return 0;
}
```

> [!warning]
>
> **Things to Watch Out For**
>
> - **Ambiguity**: If two overloads could match a call (like in Example 4), the compiler throws an error. Make sure parameter lists are unique enough.
> - **Type Conversion**: The compiler might convert types (e.g., int to double) to match an overload, which can lead to unexpected choices. Be explicit when needed.
> - **Prototypes**: If you use prototypes, all overloads need their own prototypes before use.

**Real World Use-Case:**
Imagine a calculate function for different shapes:

```cpp
#include <iostream>

double calculate(int radius) {  // Circle area
    return 3.14 * radius * radius;
}

double calculate(int length, int width) {  // Rectangle area
    return length * width;
}

int main() {
    std::cout << "Circle area: " << calculate(5) << std::endl;          // 78.5
    std::cout << "Rectangle area: " << calculate(4, 6) << std::endl;    // 24
    return 0;
}
```

### Recursive Functions


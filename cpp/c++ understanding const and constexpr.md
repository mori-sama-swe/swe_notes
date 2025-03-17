# Understanding `const` and `constexpr`

in C++, **const** and **constexpr** are two related but distinct keywords that deal with immutability and compile-time evaluation. Understanding their roles and differences is key to writing efficient and safe code. Here’s a high-level explanation:

> [!TIP]
>
> Use `const` for:
>
> - Function parameters you don’t want to modify (e.g., const std::string&).
> - Variables that shouldn’t change after initialization.
>
> Use `constexpr` for:
>
> - Constants you want computed at compile-time (e.g., constexpr int max = 100;).
> - Functions or objects you want optimized into constants when possible.
>
> Combine them wisely:
>
> - All constexpr variables are implicitly const, but not vice versa.

## `const`

#### Constant Variables

The **const** keyword ***specifies that a variable’s value cannot be modified after initialization***. It’s about **immutability** at runtime or compile-time, depending on context.

> [!NOTE] 
>
> Key Features:
>
> - **Immutable After Initialization**: Once a const variable is set, it can’t change.
> - **Scope Flexibility**: Can be used with local, global, or member variables.
> - **Runtime or Compile-Time**: The value can be determined at runtime or compile-time, depending on how it’s initialized.

Syntax and Basic Usage:

```cpp
const int max = 100; // max is constant, cannot be changed
// max = 200; // Error: assignment to const
```

#### Const With Pointers

`const int* ptr` - **Pointer to a constant integer (can’t modify the value it points to).**

```cpp
int x = 5;
const int* ptr = &x; // Can’t change x through ptr
// *ptr = 10; // Error
ptr = nullptr; // OK, pointer itself isn’t const
```

`int* const ptr` - **Constant pointer (can’t reassign the pointer, but can modify the value).**

```cpp
int y = 5;
int* const ptr = &y; // Pointer is fixed
*ptr = 10; // OK, can change y
// ptr = nullptr; // Error
```

`const int* const ptr` - **Both pointer and value are constant.**

#### Function Parameters

```cpp
void print(const int& value) { // Prevents modification of value
    // value = 20; // Error
    std::cout << value;
}
```

> [!NOTE]
>
> when to use `const` 
>
> - To prevent accidental changes to variables or parameters.
>
> - To signal intent (e.g., “this won’t change”).
>
> - For safety in function interfaces (e.g., passing large objects by const reference).

---

## constexpr

#### Compiler-Time Constant

The **constexpr** keyword (introduced in C++11) goes further by ensuring a variable or function is evaluated at **compile-time**, producing a constant expression. It’s about **performance** and **compile-time guarantees**.

> [!NOTE]
>
> Key Features:
>
> - **Compile-Time Evaluation**: The value must be computable when the code is compiled.
> - **Stronger Constness**: Implies const but enforces compile-time resolution.
> - **Broader Use**: Applies to variables, functions, and even constructors.

Syntax and Examples:

```cpp
constexpr int size = 10; // Must be known at compile-time
// constexpr int runtime = input; // Error: input isn’t compile-time

constexpr int length = 5;
int arr[length] = {1, 2, 3, 4, 5}; // Fixed size at compile-time
```

> [!NOTE]
>
> when to use `constexpr`
>
> - For performance: Compile-time computation avoids runtime overhead.
> - For constants that must be resolved early (e.g., array sizes, template arguments).
> - To enforce compile-time guarantees in complex expressions.

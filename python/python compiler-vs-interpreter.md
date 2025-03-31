# Compiler Vs Interpreter

## Compiler or Interpreter?

`python` - execution involves both `compilation` and `interpretation` : 

> [!note]
>
> **Compilation**: Python source code (what you write in a .py file) is first compiled into an intermediate form called ***bytecode***.
>
> - Bytecode is a lower-level, platform-independent set of instructions that isn’t machine code but is easier for the Python runtime to process.
>
> **Interpretation**: This bytecode is then executed by the **Python Virtual Machine (PVM)**, which interprets the bytecode instructions one by one and carries out the corresponding operations.
>
> - Python is commonly referred to as an *interpreted language* because the PVM interprets the bytecode at runtime, there’s a compilation step involved beforehand. 

## Proces of Compiling Python Code

1. source code creation 
2. lexical,syntax,semantic analysis
   - Python interpreter reads the source code and peforms lexical analysis, this breaks down the code into smaller units called **tokens**
   - the interpreter parses these tokens and check if it follow the python programming grammar rules.
3. bytecode generation
   - the intepreter compiles into bytecodes - once the analysis gets completed. **bytecode** consists of instructions that the PVM (python virtual machine) can understand, these instructions are stored in memory, in many cases they are `cached` - within a __pycache__ directory. 
     - caching speeds up the runs by skipping recompilation, if the source code hasn't changed
4. execution of the python virtual machine (PVM)
   - The PVM takes the bytecode and interprets it, executing each instruction sequentially. For instance, a bytecode instruction might tell the PVM to load a value, perform an addition, or call a function. This interpretation step is what gives Python its “interpreted” reputation.

> [!note]
>
> **Key Notes**
>
> - **Efficiency with .pyc Files**: The first time you run a script, Python generates bytecode and saves it in a .pyc file. On later runs, if the source code is unchanged, Python skips steps 2–5 and loads the bytecode directly, making execution faster.
> - **Not Machine Code**: Unlike languages like C or C++, Python doesn’t compile to machine code in its standard form. The bytecode is an abstraction that relies on the PVM, which is why Python is portable across platforms but slower than natively compiled languages.
> - **Alternative Implementations**: While CPython uses this compile-to-bytecode-then-interpret approach, other Python implementations exist. For example, PyPy uses *just-in-time (JIT) compilation* to translate bytecode to machine code at runtime for better performance, but that’s beyond the standard process.

## Dynamic or Statically Types Language?

Python is **dynamically typed**, **which means that the type of a variable is determined at runtime rather than in advance.** To understand this, let’s explore the difference between dynamic typing and static typing.

In a dynamically typed language like Python, **you don’t need to declare the type of a variable before assigning a value to it**. The type is inferred when the code runs. For example:

```python
x = 5        # x is an integer
x = "hello"  # Now x is a string
```

**Advantages of Dynamic Typing**

- **Flexibility**: You can reassign variables to different types without restrictions.
- **Simplicity**: Less boilerplate code, as no type declarations are needed.

Disadvantages

- **Runtime Errors**: Type mismatches (e.g., trying to add a string to an integer) may only be caught when the code runs.

### Static Type Explained

In contrast, **statically typed languages** like C or Java require you to declare the type of a variable before using it, and this type is checked at compile time. For example, in C:

```cpp
int x = 5;    // x is declared as an integer
x = "hello";  // This would cause a compile-time error
```

Here, the compiler ensures that x can only hold integers, and any attempt to assign a different type (like a string) is caught before the program even runs.

**Advantages of Static Typing**

- **Early Error Detection**: Type errors are caught at compile time, making the code more robust.
- **Performance**: The compiler can optimize the code based on known types.

**Disadvantages**

- **Rigidity**: You can’t easily change a variable’s type after declaring it.
- **Verbosity**: More code is needed for type declarations.

**Key Difference**

- **When Types Are Checked**: Dynamic typing (Python) checks types at runtime, while static typing (C, Java) checks them at compile time.
- **Flexibility vs. Safety**: Dynamic typing offers more flexibility but less safety, while static typing provides more safety but less flexibility.
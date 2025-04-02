# Undestanding Decorators

## what is a decorator?

A **decorator** is a function that takes another function (or method) as an argument, adds some extra behavior to it, and returns a new function. It’s a way to "wrap" or "decorate" the original function without modifying its source code directly.

> [!note]
>
> In Python, decorators are applied using the @ syntax above a function definition. They’re built on two key ideas:
>
> 1. **Functions are first-class objects**: You can pass them around, assign them to variables, or use them as arguments.
> 2. **Closures**: Inner functions can "remember" variables from their enclosing scope.

Example: a simple decorator:

```python
def my_decorator(func):
    def wrapper():
        print("Something before the function.")
        func()  # Call the original function
        print("Something after the function.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

# Call the decorated function
say_hello()

# output
Something before the function.
Hello!
Something after the function.
```

## decorators with arguments

What if the function you’re decorating takes arguments? You need to modify the wrapper to handle them:

Decorators are useful for:

- **Code reuse**: Apply the same modification (e.g., logging, timing, caching) to multiple functions.
- **Separation of concerns**: Keep extra functionality (like validation or error handling) separate from core logic.
- **Readability**: The @ syntax makes it clear what’s being added to a function.

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before the function.")
        result = func(*args, **kwargs)  # Pass arguments to the original function
        print("After the function.")
        return result  # Return the result
    return wrapper

@my_decorator
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))


# Output
Before the function.
After the function.
Hello, Alice!
```

> [!Important]
>
> ### Summary
>
> - **Decorators** modify functions by wrapping them with extra behavior.
> - They use closures and Python’s first-class function support.
> - Syntax: @decorator above a function definition.
> - With arguments: Use a factory function (e.g., def cached(cache)).
> - Practical uses: Logging, timing, caching (like @cached), authentication, etc.
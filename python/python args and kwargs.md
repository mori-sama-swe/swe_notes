# Args and Kwargs

In Python, `*args` and `**kwargs` are special syntaxes used in **function definitions to handle a variable number of arguments.** 

- **They make functions more flexible by allowing you to pass an arbitrary number of positional and keyword arguments without defining them explicitly in advance.** Let’s break them down:


## *args (Arbitary Positional Arguments)

> [!note]
>
> The `*args` **parameter allows a function to accept any number of positional arguments.**
>
> - **The asterisk (*) unpacks an iterable (like a list or tuple) into individual arguments.**
>
> - Inside the function, args is treated as a tuple containing all the positional arguments passed.

```python
def print_args(*args):
    for arg in args:
        print(arg)

print_args(1, 2, 3, "hello")

#output
1
2
3
hello
```

Here, *args collects all the arguments (1, 2, 3, "hello") into a tuple, and the function iterates over them.

> [!note]
>
> Key Points:
>
> - The name args is just a convention; you could use *anything, but args is widely recognized.
> - It’s useful when you don’t know how many arguments will be passed.

## **kwargs (Arbitrary Keyword Arguments)

The `**kwargs` **parameter allows a function to accept any number of keyword arguments (i.e., arguments specified with a key-value pair).**

> [!note]
>
> - **the double asterisk (**) unpacks a dictionary into keyword arguments.**
> - Inside the function, **kwargs is treated as a dictionary containing the keyword arguments.**

```python
def print_kwargs(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_kwargs(name="Alice", age=30, city="New York")

#output:
name: Alice
age: 30
city: New York
```

Here, `**kwargs` collects the keyword arguments (name="Alice", age=30, city="New York") into a dictionary.

> [!note]
>
> **The name kwargs is a convention; you could use **anything, but kwargs is standard.**
>
> - It’s useful for passing named parameters dynamically.

## Combining `*args` and `**kargs`

You can use both in the same function. The order matters: *args must come before **kwargs.

```python
def combine_example(*args, **kwargs):
    print("Positional args:", args)
    print("Keyword args:", kwargs)

combine_example(1, 2, 3, name="Bob", job="Engineer")

#output:
Positional args: (1, 2, 3)
Keyword args: {'name': 'Bob', 'job': 'Engineer'}
```

Practical Use Cases

1. `*args:`
   - When writing a function like sum() that can take any number of numbers.
   - Example: def my_sum(*args): return sum(args)
2. `**kwargs:`
   - When creating functions that need optional parameters with defaults or configurations.
   - Example: A function to build a user profile with flexible attributes.
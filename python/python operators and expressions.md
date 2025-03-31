# Operators and Expressions

## Arithmetic Operators

> [!note]
>
> **Key Points:**
>
> - Division (/) always returns float, floor division (//) returns int if both operands are int
> - Operations between int and float result in float
> - Watch out for ZeroDivisionError with / and //
> - Modulus with negative numbers follows the formula: a % b = a - b * (a // b)
> - Use parentheses to control order of operations

practical examples:
```python
# Calculate circle area (πr²)
import math
radius = 5
area = math.pi * radius ** 2
print(f"Area: {area:.2f}")  # Output: Area: 78.54

# Convert seconds to hours, minutes, seconds
total_seconds = 3665
hours = total_seconds // 3600
minutes = (total_seconds % 3600) // 60
seconds = total_seconds % 60
print(f"{hours}h {minutes}m {seconds}s")  # Output: 1h 1m 5s
```

```python
# Basic addition
x = 5 + 3    # Result: 8
y = 2.5 + 1.7 # Result: 4.2

# String concatenation
text = "Hello" + " World"  # Result: "Hello World"

# Basic subtraction
x = 10 - 4    # Result: 6
y = 5.5 - 2.3  # Result: 3.2

# Unary minus
z = -5        # Result: -5
neg = -(10 - 4)  # Result: -6

# Basic multiplication
x = 4 * 3     # Result: 12
y = 2.5 * 2   # Result: 5.0

# String/list repetition
text = "Hi" * 3    # Result: "HiHiHi"
items = [1, 2] * 2 # Result: [1, 2, 1, 2]

# Basic division
x = 10 / 2    # Result: 5.0
y = 7 / 2     # Result: 3.5

# Division with negative numbers
z = -10 / 2   # Result: -5.0

# Be careful with zero!
# w = 5 / 0   # Raises ZeroDivisionError

# Basic floor division
x = 7 // 2    # Result: 3
y = 10 // 3   # Result: 3

# With negative numbers
z = -7 // 2   # Result: -4 (rounds down)
w = 7 // -2   # Result: -4

# Basic modulus
x = 10 % 3    # Result: 1
y = 7 % 2     # Result: 1

# With negative numbers
z = -10 % 3   # Result: 2
w = 10 % -3   # Result: -2

# Basic exponentiation
x = 2 ** 3    # Result: 8
y = 3 ** 2    # Result: 9

# Fractional exponents (roots)
z = 16 ** 0.5 # Result: 4.0 (square root)
w = 8 ** (1/3) # Result: 2.0 (cube root)
```

Example with multiple operators:

```python
result = 2 + 3 * 4 ** 2  # Evaluates as 2 + (3 * (4 ** 2))
# 1. 4 ** 2 = 16
# 2. 3 * 16 = 48
# 3. 2 + 48 = 50
print(result)  # Output: 50

# With parentheses
result2 = (2 + 3) * 4 ** 2
# 1. (2 + 3) = 5
# 2. 4 ** 2 = 16
# 3. 5 * 16 = 80
print(result2)  # Output: 80
```




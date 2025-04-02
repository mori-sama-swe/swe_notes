# PYTEST

documents: https://docs.pytest.org/en/stable/how-to/assert.html

### what is fixtures?

**fixture**: a method is automatically used for all test in the class, it also sets up dependencys required to run the tests (database connection/client) 

---

### what is assert?:

The `assert` statement in pytest is a built-in Python keyword used to verify that a condition is true.

```python
def test_addition():
    assert 1 + 1 == 2  # This passes because 1 + 1 equals 2
```

---

### Raises For Exception Testing

Instead of using `assert` to check if an exception is raised, you can use pytest.raises, a context manager designed specifically for testing exceptions.

`pytest.raises` is a context manager provided by the pytest framework to test whether a specific exception is raised when a block of code runs. **If the expected exception occurs, the test passes.** **If it doesn’t occur—or if a different exception is raised—the test fails.** It’s a cleaner, more explicit alternative to manually catching exceptions with try/except and using assert.

```python
import pytest

with pytest.raises(ExceptionType):
    # Code that should raise the specified exception
```

**ExceptionType**: The type of exception you expect (e.g., ValueError, TypeError, ZeroDivisionError).

**The with block**: Contains the code you’re testing. If it raises the expected exception, the test passes.

example:
```python
def divide(a, b):
    return a / b

def test_divide_by_zero():
    with pytest.raises(ZeroDivisionError):
        divide(1, 0)
```

---

> [!note]
>
> "How do I write a test that *passes* if an exception is raised (any exception), and *fails* if no exception is raised?"
>
> - **Pass**: If *any* exception is raised.
> - **Fail**: If no exception is raised.
>
> Solution: Using pytest.raises with a Broad Exception
>
> The simplest way is to use pytest.raises with the base Exception class, which catches almost all exceptions (excluding rare cases like SystemExit or KeyboardInterrupt). Then, we let the test fail naturally if no exception occurs.
>
> ```python
> import pytest
> 
> def risky_function():
>     # This could raise an exception... or not
>     return 1 / 0  # Example: raises ZeroDivisionError
> 
> def test_exception_happens():
>     with pytest.raises(Exception):
>         risky_function()
> ```
>
> 


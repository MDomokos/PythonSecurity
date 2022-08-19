# Bonus non security tip: Use Python type annotations

With version 3.5, [type hints](https://docs.python.org/3/library/typing.html) were introduced. While the Python runtime does not enforce type annotations, tools such as type checkers, IDEs, linters, SASTs, and others can benefit from the developer being more explicit. Here is an example to highlight the idea:

```python
MODE = Literal['r', 'rb', 'w', 'wb']
def open_helper(file: str, mode: MODE) -> str:
    ...
open_helper('/some/path', 'r')  # Passes type check
open_helper('/other/path', 'typo')  # Error in type checker
```

[Literal[…]](https://www.python.org/dev/peps/pep-0586/) was introduced with version 3.8 and is not enforced by the runtime (you can pass whatever string you want in our example) but type checkers can now discover that the parameter is outside the allowed set and warn you. This is a great piece of functionality, and not just for Python security.

**Note:** As it is not enforced by the runtime, the security usage of type hints is limited.
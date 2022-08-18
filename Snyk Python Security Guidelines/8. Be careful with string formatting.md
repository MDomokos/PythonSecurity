# Be careful with string formatting

Despite Python’s idea of having one — and only one — way to do things, it actually has four different ways to format strings (three methods for versions prior to Python 3.6).

String formatting has gotten progressively more flexible and powerful (f-strings are particularly interesting), but as flexibility increases, so does the potential for exploits. For this reason, Python users should carefully consider how they format strings with user-supplied input.

Python has a built-in module named `string`. This module includes the `Template` class, which is used to create template strings.

Consider the following example.

```python
from string import Template
greeting_template = Template(“Hello World, my name is $name.”)
greeting = greeting_template.substitute(name=”Hayley”)
```

For the above code, the variable greeting is evaluated as: “Hello World, my name is Hayley.”

This string format is a bit cumbersome because it requires an import statement and is less flexible with types. It also doesn’t evaluate Python statements the way f-strings do. These constraints make template strings an excellent choice when dealing with user input.

Another quick note about string formatting: Be extra careful with raw SQL as mentioned above.
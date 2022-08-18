# Use Python virtual environments

Python is equipped to separate application development into virtual environments. A virtual environment isolates the Python interpreter, libraries, and scripts installed into it. This means that instead of using a global Python version and global Python dependencies for all your projects, you can have project-specific virtual environments that can use their own Python (and Python dependency) versions!

Most IDEs, CLIs, and dashboards such as [Anaconda Navigator](https://www.anaconda.com/products/individual) have built-in functions to switch between virtual environments.

**Pro Tip:** As of Python version 3.5, the use of `venv` is recommended and with version 3.6 `pyvenv` was deprecated.

Virtual environments make developing, packaging, and shipping secure Python applications easier. Using them is highly recommended. See [the Python venv doc for more details](https://docs.python.org/3/library/venv.html).
# Be careful when downloading packages

It is easy to install packages, but they’re also an easy way to introduce Python security vulnerabilities. Typically, developers use the standard package installer for Python (pip) which uses the Python Pack Index (PyPI). This makes it important to understand how packages are added to PyPI.

[PyPI has a procedure](https://pypi.org/security/) for reporting security concerns. If someone reports a malicious package, or a problem within PyPI, it is addressed, but packages added to PyPI do not undergo review — this would be an unrealistic expectation of the volunteers who maintain PyPI.

Therefore, it is wise to assume that there are malicious packages within PyPI and you should act accordingly. Reasonable steps include doing a bit of research on the package you want to install and ensuring that you carefully spell out the package name ([a package named for a common misspelling of a popular package could execute malicious code](https://www.theregister.com/2021/03/02/python_pypi_purges/)). Before downloading a package, make sure to check it on [Snyk Advisor](https://snyk.io/advisor/).

Doing a quick search for a package on Snyk Advisor gives you a lot of information on the package, its support in the community, its history of bugs and fixes, and a lot more. Snyk Advisor also provides the installation command at the top of the result page. It is a best practice to copy and paste that spelling to prevent [typosquatting](https://snyk.io/blog/typosquatting-attacks/). Snyk Advisor can tell you whether or not you should trust a package. You can see the history of security issues and the time it took to get them fixed. 

Another best practice is to use virtual environments to isolate projects from each other. Also, use `pip freeze` or a comparable command to record changes in the environment in the [requirement list](https://pip.pypa.io/en/stable/user_guide/#requirements-files).

Maintaining references in an up-to-date manner, [Snyk Open Source](https://snyk.io/product/open-source-security-management/) is based on an industry-leading [vulnerability database](https://security.snyk.io/) recording security issues and possible fixes. Snyk Open Source runs scans using the requirements and provides actionable information about discovered vulnerabilities of direct and transitive dependencies and helps you to fix them right away.
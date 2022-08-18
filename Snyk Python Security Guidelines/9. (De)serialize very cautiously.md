# (De)serialize very cautiously

Python provides a built-in mechanism to serialize and deserialize Python objects called “pickling” using the [pickle](https://docs.python.org/3/library/pickle.html) module. This is known to be insecure and it is advisable to **use it very cautiously and only on trusted data sources**.

The new de facto standard for serialization/deserialization is YAML. The [PyYAML](https://pypi.org/project/pyaml/)package provides a mechanism to serialize custom data types to YAML and back again. But PyYAML is riddled with various [possible attack vectors](https://snyk.io/vuln/pip:PyYAML). A simple but effective way to secure the usage of PyYAML is using `yaml.SafeLoader()` instead of `yaml.Loader()` as a loader.

```python
Data = yaml.load(input_file, Loader=yaml.SafeLoader)
```

This prevents loading of custom classes but supports standard types like hashes and arrays.

Another typical use case is XML. Standard libraries are often used but are vulnerable to [typical attacks](https://docs.python.org/3/library/xml.html#xml-vulnerabilities) — namely DOS attacks or external entity expansion (an external source is references). A good first line of defense is a package called [defusedxml](https://snyk.io/advisor/python/defusedxml). It has safeguards against these typical XML security issues.
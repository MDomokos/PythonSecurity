# Always sanitize external data

One vector of attack for any application is external data, which can be used for injection, [XSS](https://snyk.io/learn/cross-site-scripting/), or denial of service (DOS) attacks. A general rule for maintaining Python security is to always sanitize data (remove sensitive information) from external sources whether the data originates from a user input form, scraping a website, or a database request. Also, sanitize as soon as the data enters the application to prevent insecure handling. This reduces the risk that unsanitized sensitive data will be handled by your application accidentally. 

Starting with sanitization, it always makes more sense to check for what the input should be than to [try to handle the exceptions](https://www.advancedcyber.co.uk/it-security-blog/phishing-technique-certainly-vulnerable-to). We also recommend using well-maintained libraries for sanitization. Here are two:

-   [schema](https://pypi.org/project/schema/) is “a library for validating Python data structures, such as those obtained from config-files, forms, external services or command-line parsing, converted from JSON/YAML (or something else) to Python data-types.
-   [bleach](https://pypi.org/project/bleach/) is “an allowed-list-based HTML sanitizing library that escapes or strips markup and attributes.” 

Major frameworks come with their own sanitation functions, like [Flask](https://flask.palletsprojects.com/en/2.0.x/api/?highlight=escape#flask.escape)’s `flask.escape()` or [Django](https://docs.djangoproject.com/en/2.0/_modules/django/utils/html/)’s `django.utils.html.escape()`. The goal of any of these functions is to secure potentially malicious HTML input like:

```python
>>> import bleach
>>> bleach.clean('an XSS <script>navigate(...)</script> example')
'an XSS &lt;script&gt;navigate(...)&lt;/script&gt; example'
```

The limitation of this approach is that libraries are not good for everything. They are specialized in their domain. As a note, be sure to read to the end of this post to get more information about working with other data formats, such as XML, which can also contain malicious data.

Another often used option is to leave the rendering of HTML to templating engines such as [Jinja](https://jinja.palletsprojects.com/en/3.0.x/). It provides lots of capabilities, and amongst them is [auto-escaping to prevent XSS](https://jinja.palletsprojects.com/en/3.0.x/intro/) using [MarkupSafe](https://markupsafe.palletsprojects.com/en/2.0.x/).

Another aspect of sanitization is preventing data from being used as a command. A typical example is an [SQL injection](https://snyk.io/learn/sql-injection/). Instead of stitching strings and variables together to generate an SQL query, it is advisable to use named-parameters to tell the database what to treat as a command and what as data. 

```python
# Instead of this …
cursor.execute(f"SELECT admin FROM users WHERE username = '{username}'");
# ...do this...
cursor.execute("SELECT admin FROM users WHERE username = %(username)s", {'username': username}); 
```

Or even better, use Object-Relational Mapping (ORM), such as [sqlalchemy](https://www.sqlalchemy.org/), which would make the example query look like this:

```python
query = session.query(User).filter(User.name.like('%{username}'))
```

Here you get more readable code, as well as ORM optimizations like caching, plus more security and performance!

If you want to learn more, check out our [SQL injection cheat sheet](https://snyk.io/blog/sql-injection-cheat-sheet/).
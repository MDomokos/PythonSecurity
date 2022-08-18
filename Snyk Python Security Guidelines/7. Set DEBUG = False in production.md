In a development environment, it makes sense to have verbose error messages. In production though, you want to prevent any leaks of information that might help an attacker to learn more about your environment, libraries, or code. 

By default, most frameworks have debugging switched on. For example, Django has it enabled in settings.py. Make sure to switch debugging to `False` in production to prevent leaking sensitive application information to attackers.

**Pro Tip:** When deploying to production, it is useful to have your continuous deployment system verify this setting is disabled post-deployment.
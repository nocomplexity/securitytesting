# Injection Attacks

### Finding `eval()`, `exec()`, and Insecure SQL Queries

Injection occurs when untrusted input is treated as code or as part of a command. In Python, this most often manifests in three ways:

* Dynamic code execution (`eval`, `exec`)
* Shell command execution
* Unsafely constructed SQL queries



### Dangerous Dynamic Execution: `eval()` and `exec()`

Both `eval()` and `exec()` execute strings as Python code.

```python
user_input = input("Enter calculation: ")
result = eval(user_input)
print(result)
```

If a user enters:

```python
__import__("os").system("rm -rf /")
```

When using Python Code Audit with do the command:
```bash
codeaudit filescan eval_sample.py
```

You see that the findings are:

![sast-findings-input](/images/input_sample.png)

Both `input` and `eval` are detected; since both can be exploited, identifying them is essential. This ensures that when using **Python Code Audit**, the detection of common injection attacks is fully supported.



You have remote command execution.

### What to Look for in SAST findings

Use of:
* `eval()`
* `exec()`
* `compile()`
* `input(` and Any dynamic execution involving user-controlled input
* Template engines that can be misused to execute logic

Since no SAST for Python will detect anything that might cause weakness, be alert on:
* Alerts found by Python Code Audit regarding external Egress Risk.
* f-strings or string concatenation passed into dangerous functions

:::{danger} 
Dynamic execution turns input validation errors into **arbitrary code execution vulnerabilities**, often leading to full compromise.
:::


## Insecure SQL Queries

A common pattern in Python applications using SQLite, MySQL, or PostgreSQL:

```python
query = f"SELECT * FROM users WHERE username = '{username}'"
cursor.execute(query)
```

If `username` is:

```sql
admin' OR '1'='1
```

The attacker bypasses authentication.

## What to Look for

* f-strings building SQL
* `%` string formatting in queries
* `.format()` used in SQL statements
* Concatenation (`+`) used to construct queries

## Secure Alternative

```python
cursor.execute("SELECT * FROM users WHERE username = ?", (username,))
```

Or with libraries such as **SQLAlchemy**, using parameterised queries or ORM query builders.

## Testing Techniques

* Fuzz input fields with:

  * `' OR 1=1--`
  * `' UNION SELECT NULL--`
* Use automated scanners (e.g. **sqlmap**) in controlled environments.
* Inspect logs for malformed SQL errors.

:::{note} 
**Python Code Audit** does not perform analysis or reporting on possible injection attacks.

However, **Python Code Audit** is still a valuable aid for detecting code constructs that must be analysed in depth.
Python Code Audit assists in mitigating injection attacks by:

- Discovering the use of database libraries.

- Identifying known vulnerabilities within those libraries.
...and more!

Testing for injection attacks in Python code should be conducted using tools such as:

- Specialised FOSS (Free and Open Source Software) tools.
- Advanced fuzzers
:::

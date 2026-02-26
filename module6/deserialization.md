# Insecure Deserialization

## The Dangers of `pickle` and `yaml.load`

Deserialization vulnerabilities arise when applications reconstruct objects from untrusted data.

In Python, this is particularly dangerous with:

* `pickle`
* `yaml.load` (without safe loader)


### `pickle`: Arbitrary Code Execution by Design

`pickle` is not secure against untrusted input.

```python
import pickle

data = request.data
obj = pickle.loads(data)
```

An attacker can craft a malicious pickle payload that executes arbitrary system commands during deserialization.


The `pickle` protocol allows objects to define how they are reconstructed, including calling arbitrary callables.

If untrusted users control pickled data, they control code execution.

:::{tip} 
When using **Python Code Audit**, any use of pickle will be detected.
:::


### Unsafe YAML Loading

Older versions of PyYAML allowed this:

```python
import yaml

data = yaml.load(user_input)
```

Without specifying a safe loader, this could instantiate arbitrary Python objects.

### Secure Alternative

```python
yaml.safe_load(user_input)
```

### What to Look for in Audits

* `yaml.load(` without `Loader=`
* `FullLoader` used unnecessarily
* Deserialization of configuration files controlled by users
* Upload-and-parse workflows


Attackers upload a “configuration file” that is actually a malicious object constructor.

:::{note} 
**Python Code Audit** is designed not to detect the insecure use of third-party libraries automatically.

However, by using the provided APIs, it is straightforward to create custom scanning rules for any third-party library calls you wish to avoid.
:::


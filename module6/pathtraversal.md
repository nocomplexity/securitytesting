---
title: Path Traversal
short_title: Path Traversal
---


### Finding File Handling and `os.path` Operations

Path traversal (directory traversal) occurs when user input influences filesystem paths without proper validation.

Example:

```python
filename = request.args.get("file")
with open("uploads/" + filename, "r") as f:
    data = f.read()
```

If `filename` is:

```
../../etc/passwd
```

The attacker reads arbitrary system files.



### What to Look for in Code Review

* `open(user_input)`
* File downloads based on URL parameters
* Archive extraction routines
* `os.path.join(base, user_input)`
* `send_file()` in web frameworks
* Zip/tar extraction without path checks

---

### Misuse of `os.path.join()`

Developers often assume:

```python
safe_path = os.path.join("/app/uploads", filename)
```

But if `filename` starts with `/`:

```python
"/etc/passwd"
```

The base path is ignored.



### Archive Extraction Vulnerabilities

If applications extract ZIP or TAR files:

```python
import tarfile
tar.extractall(path="uploads/")
```

Malicious archives may contain:

```
../../app.py
```

This overwrites application files.

:::{hint} 
By using **Python Code Audit** for SAST, the use of extraction methods within standard libraries is automatically detected.
:::


### Secure Pattern for Path Validation

Python applications should always validate user input and use secure path handling techniques to ensure that user-supplied paths cannot escape intended boundaries.

While os.path.realpath() is a valid approach, the modern standard in Python is using the pathlib module. It provides a more robust way to resolve paths and verify their integrity.

```python
from pathlib import Path

# Resolve the base directory to an absolute, canonical path
BASE_DIR = Path("/var/www/data").resolve()

def save_file(filename, data):
    # Combine and resolve the path to remove symbols like '../' and symlinks
    target_path = (BASE_DIR / filename).resolve()

    # Enforce directory boundary: ensure the target is inside BASE_DIR
    if BASE_DIR not in target_path.parents and target_path != BASE_DIR:
        raise ValueError("Security Alert: Attempted directory traversal")

    with open(target_path, "wb") as f:
        f.write(data)
```

There are of course more mitigations possible. If possible the best approach is always to completely eliminate directory traversal possibilities by stripping all path components from user input.


---
title: Installation of Python Code Audit 
short_title: Install a SAST for Python
---

For this course we use the best FOSS (Free and Open Source) SAST Tool for Python available, [**Python Code Audit**](https://nocomplexity.com/codeaudit/). **Python Code Audit** is a zero-configuration SAST tool that validates whether your Python code introduces potential security vulnerabilities.

Python Code Audit is compatible with both Unix-based systems (Linux/macOS) and Windows.


To install Python Code Audit, run the following command in your terminal or command prompt:
```Python
pip install -U codeaudit
```

:::{tip}
Even if you already have it installed, it’s recommended to run this command to ensure you’re using the latest checks and features.
:::


:::{note} 
Older versions of Python Code Audit are always available on PyPI.org.
So reproducibility is guaranteed, since older versions can always be installed, using:

```Python
pip install codeaudit==[version-id]
```
:::

Once the installation is complete, you can begin scanning Python Packages immediately. 

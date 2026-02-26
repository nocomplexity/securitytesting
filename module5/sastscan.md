---
title: Static Application Security Test (SAST) to find weakness in Python Code
short_title: SAST scan
---

## Overview

Running a Static Application Security Test (SAST) on Python code is essential for ensuring security. It is also a straightforward [shift-left practice](https://nocomplexity.com/documents/simplifysecurity/intro.html#)  that takes only a fraction of your time yet can help you avoid serious security incidents.


Python Code Audit scans and checks for **potential security issues**. A potential security issue is a weakness that **can** lead to a security vulnerability with impact.

There is an important difference between a **potential security issue** and a **security vulnerability** in Python code:

:::{important} 
A **potential security issue** or weakness is a general flaw, error, mistake or sloppy programming habit in a programs design, implementation, or operation that could lead to security problems. It's a potential area of concern that might not be immediately exploitable but increases the risk of a vulnerability emerging. 

Depending on the **context** where a Python program is executed, found security issues should be fixed, or can be neglected. 
:::

Examples of **potential security issues** or weaknesses that Python Code Audit discovers:
* Risks of running untrusted code by using Python statements that allow this. Think of `compile`, `eval` or `exec`.
* Availability risks. Operating systems functions that can create directories or files can cause availability risks.
* Risks of changing permission on files or directories. Python files are too often run with too broad permissions. This can lead to severe risks on data leakage or integrity issues on files.


Issues in Python code are not necessarily directly exploitable on their own, but detected security issues are a fertile ground for vulnerabilities to appear.

:::{admonition} What is a vulnerability? 
:class: tip
A vulnerability is an exploitable weakness in a system, application, or process.

Security testing helps to minimise the risk posed by vulnerabilities, as appropriate mitigation measures can be identified and implemented where necessary.
:::

:::{danger} 
If a weakness in Python code exists, and **if** a method is found to take advantage of that weakness to cause harm, then it becomes a vulnerability. 

Addressing weaknesses [proactively](https://nocomplexity.com/documents/simplifysecurity/shiftleft.html#shift-left) helps prevent vulnerabilities from emerging, while patching vulnerabilities reactively addresses known exploitable flaws.
:::

## How to start a SAST scan on Python code


On the command line do:
```bash
codeaudit filescanscan <package-name|directory|file> [reportname.html]
```

You can chose a custom report name. But make sure it ends with `.html` since a the report is a static html file.

## What security validations are done?

By running the command:
```bash
codeaudit filescanscan <package-name|directory|file> [reportname.html]
```

An automatic security test is done on a Python package or file to determine:
1. If common security weaknesses based on standard Python library use are present. The default list used for validation is based on more than 85 Python constructs that can cause vulnerabilities depending on the exact context a program is executed and used.
2. Analysis of security relevant file details.See section on [Complexity check](complexitycheck) on all matrix that are determined.
3. Used modules in per file. If needed always validate if known security vulnerabilities in third party modules are present. Use the **Python Code Audit** modulescan command for this. See also section on [Checking Python dependencies](dependency_checking).
4. If there is an external Egress Risk. **Python Code Audit** checks for Possible API keys or logic for connecting to remote services in the code. 
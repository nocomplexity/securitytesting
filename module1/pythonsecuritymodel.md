---
title: Python Security model
short_title: Python Security model
---


The emphases in this course is on security testing for Python programs. But if you want to learn more about Secure Coding  for Python , check the Secure [Coding Guidelines for Python](https://nocomplexity.com/documents/codeaudit/securecoding.html#secure-coding-guidelines).

![Python Security Model](/images/pythonsecuritymodel.png)

## The Core Python Security Model

To effectively protect Python applications against malware and other threats, it is essential to understand Python’s core security model. 

:::{danger} 
Security in Python is not enforced by strict isolation at the language level; rather, it relies heavily on developer awareness, correct configuration, and disciplined coding practices.

**Security testing is critically important!**
:::

### Memory Management and Process Safety

Unlike lower-level languages such as C or C++, Python abstracts direct memory access away from the developer. This significantly reduces the likelihood of memory corruption vulnerabilities such as buffer overflows, dangling pointers, or arbitrary memory writes.

Python manages memory through:

* **Reference counting**
* **Automatic garbage collection**

These mechanisms prevent many classic memory exploitation techniques. However, they do not eliminate risk entirely. From a security perspective, you must still consider:

* Resource exhaustion (e.g. memory leaks caused by unintended object retention)
* Denial-of-service risks through excessive object creation
* Abuse of large in-memory data structures

Python protects against direct memory manipulation, but it does **not protect against logic flaws or resource misuse**.



### Code Execution Model and the Python Virtual Machine

Python source code is compiled into **bytecode**, which is then executed by the **Python Virtual Machine (PVM)** within the interpreter process.

This execution model has important security implications:

* All imported modules execute within the same interpreter process.
* There is no built-in sandbox for untrusted code.
* Malicious code in dependencies runs with the same privileges as the application itself.

If an attacker can influence what code is imported or executed, they can potentially execute arbitrary instructions within the application’s trust boundary.

For this reason, protecting against malware in Python requires:

* Strict dependency management
* Careful control of execution environments
* Isolation using containers or virtual environments
* Least-privilege operating system permissions


### Dynamic Behaviour and Security Risks

Python is highly dynamic. This flexibility is powerful, but it also increases the attack surface.

Key dynamic features include:

* **Dynamic typing**
* **Reflection and introspection**
* **Runtime code execution (`eval`, `exec`)**
* **Dynamic imports**
* **Monkey patching**

From a **malware defence perspective,** these features introduce risks such as:

* Code injection
* Execution of untrusted input
* Hidden or obfuscated behaviour
* Manipulation of runtime objects
* Bypassing of security checks

For example, executing user input through `eval()` or `exec()` can lead directly to remote code execution vulnerabilities. Similarly, unsafe deserialisation of data can result in arbitrary object creation and code execution.

Python does not restrict these behaviours by default. The responsibility for safe use lies with the developer.


### Trust Boundaries and Attack Surface

A core part of Python’s security model is understanding **trust boundaries**:

* User input is untrusted.
* External APIs are untrusted.
* Third-party libraries may be compromised.
* Deserialised data must be treated as hostile.

Python’s import system, packaging ecosystem, and dynamic execution capabilities mean that the attack surface often extends beyond the application’s own source code. Supply chain attacks, malicious packages, and dependency confusion attacks are real threats in Python environments.

Protecting against malware therefore requires:

* Verifying dependencies
* Pinning package versions
* Reviewing high-risk libraries
* Monitoring for known vulnerabilities
* Running applications in controlled, isolated environments



### No Built-in Sandbox

It is important to understand that Python **does not** provide a secure sandbox environment for executing untrusted code. Attempts to “restrict” Python by removing certain built-ins or blocking modules are generally insufficient and can often be bypassed.

True isolation must be implemented at the operating system or infrastructure level, for example using:

* Containers
* Virtual machines
* Process isolation
* Mandatory access controls



## Security Responsibility in Python

Python reduces certain low-level risks through abstraction and managed memory. However, it does not enforce strict runtime security boundaries. Its philosophy prioritises flexibility and developer productivity over restrictive security controls.

From a security testing perspective, this means:

* Python security testing is essential.
* From a testing perspective you must evaluate how external input influences execution of code.
* Security auditing and testing means you must analyse dependency risk.
* Security auditing and testing can also involves determining assess privilege levels and validating security of runtime environments.

Understanding Python’s internal execution model, memory handling, and dynamic capabilities allows you to reason about how malware could execute, how attackers could cross trust boundaries, and how to design effective defensive controls.


:::{note} 
**Strong security for Python applications is not automatic — it is engineered.**
:::

:::{caution}
Many Python frameworks prioritize ease of use over strict security in their default configurations (e.g., debug mode in Flask/Django). Moving to a "hardened" production state is a manual, engineered process.
:::
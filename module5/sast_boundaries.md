---
title: SAST Boundaries - What Can and Cannot Be Detected?
short_title: SAST Boundaries 
---

Static Application Security Testing (SAST) is one of the core techniques in Python security testing. It analyses source code without executing it, identifying patterns, data flows, and potentially dangerous constructs.

However, SAST is not magic.

Understanding its capabilities and limitations is critical if you are to use it effectively — or assess its results correctly during an engagement.

## SAST Boundaries: What Can and Cannot Be Detected?

Static Application Security Testing (SAST) is one of the **core techniques in Python security testing**. It analyses source code *without executing it* to detect potentially dangerous constructs.

However, no SAST tool for Python is not magic.

Understanding its **capabilities and limitations** is critical if you are to use it effectively — or assess its results correctly during an engagement.


Each works slightly differently, but they all share a fundamental constraint:

:::{caution} 
SAST can only reason about what it can *see in the code*.
:::


## What SAST Can Detect Reliably

### Known Dangerous Function Usage

SAST excels at spotting dangerous functions and commonly known weaknesses in function use. For example, **Python Code Audit** and most SAST tools can detect things like:

* `eval()`, `exec()`
* `pickle.loads()`
* Various forms of `subprocess` uses that can lead to injection vulnerabilities.
* Weak hashes like MD5 or SHA1

Example:

```python
import subprocess
subprocess.call(user_input, shell=True)
```

This dangerous line is always detected. Even if mask by using e.g.: 
```Python
from subprocess import call as safefriend
safefriend(user_input, shell=True)
```

:::{caution} 
Most commercially used SAST scanners for Python rely on pattern-detection rules that require manual configuration.

By default, the functionality of these kinds of SAST scanners is **very limited(!!)**. To be effective, you must design and configure bespoke rule sets yourself.

**Python Code Audit** includes a very rich rule set by default, relieving you of the difficult task of defining meaningful rules for detecting code weaknesses.
:::

## Where SAST Starts to Struggle

Understanding these limitations is what separates a competent tester from a checkbox operator.



### Runtime-Dependent Behaviour

SAST tools do not execute code. So it cannot see:

* Actual runtime values
* Database contents
* Environment variables
* Feature flags
* Deployment configuration differences

Example:

```python
if settings.DEBUG:
    enable_admin_console()
```

If `DEBUG` is set via an environment variable at deployment time, SAST may not know the production value.



### Dynamic Code Execution

Python is highly dynamic.

SAST struggles with:

* Dynamic imports
* Reflection (`getattr`, `setattr`)
* Metaclasses
* Decorator chains
* Monkey patching
* Plugin architectures

Example:

```python
module = __import__(user_input)
```

If the module name is derived indirectly across multiple files, many SAST engines will lose track of it.

:::{tip} 
If you use Python Code Audit, the `_import__` call is detected by design.

This because Importing modules dynamically to execute code can load untrusted code.
:::

### Complex Data Flow Across Boundaries

Large applications distribute logic across:

* Multiple modules
* Microservices
* Background workers
* Message queues
* External APIs

SAST tools may fail to:

* Track taint across service boundaries
* Understand deserialisation in one component and execution in another
* Identify vulnerabilities that only emerge when systems interact

:::{tip} 
Use **Python Code Audit**, as it will detect whether logic for connecting to remote services is present.

However, it is up to you, the security tester, to carry out a manual review and determine whether this weakness should genuinely be classified as a vulnerability.
:::




### Business Logic Vulnerabilities

SAST tools cannot understand *intent*.

It cannot detect:

* Broken access control
* Privilege escalation through logic flaws
* Race conditions
* Economic abuse scenarios
* Abuse of intended functionality

Example:

```python
if user.is_authenticated:
    delete_account(target_user)
```

The issue may not be technical — it may be missing an authorisation check.
SAST may not understand the application's access model.

---

### Context-Sensitive SQL Injection

If sanitisation depends on runtime logic:

```python
if safe_mode:
    username = escape(username)
```

If `safe_mode` is influenced elsewhere, SAST may:

* Flag false positives
* Miss real vulnerabilities
* Fail to reason about conditional flows


### Correct Third-Party Library Usage

Many Python Third-Party Library modules are broken by design.

A simple and good way to get a quick insight in the security quality is to:
1. Run:
```bash
codeaudit filescan [package-name]
```
2. Check the package for known vulnerabilities:
```bash
codeaudit modulescan [package-name]
```



## What SAST Cannot Detect

SAST tools, such as Python Code Audit, excel at static code analysis to identify security weaknesses. Please also refer to [Module 2](module2/testselection) for other tools required for Python security testing.

Due to the inherent limitations of static analysis, SAST tools cannot identify reliability issues that may impact availability—a crucial aspect of security.

Types of issues that can not be detected by using only SAST scanners:

1. Authentication Bypass via Logic Errors

2. Race Conditions

3. Timing Attacks

4. Memory Exhaustion via Resource Abuse

5. Production-Only Misconfiguration

6. Infrastructure-Level Weaknesses

7. Exploitable Debug Endpoints Exposed by Deployment

:::{caution}
SAST testing alone is insufficient.
:::

Good security testing means also validation on:

* If security-by-design is applied and a minimum security baseline is implemented.
* Actual runtime values
* User interaction sequences
* Environmental configuration
* Business rules
* Integration aspects, like cross-service interactions from a security point of view.


## The Testing Mindset: Using SAST Correctly

SAST should be treated as:

* A **triage assistant**
* A **pattern detector**
* A **code review accelerator**
* Not a substitute for human reasoning

Effective workflow:

1. Run SAST early and often.
2. Investigate critical sinks manually.
3. Perform targeted manual review of:

   * Authentication
   * Authorisation
   * Deserialisation
   * File handling
4. Combine with:

   * DAST (Dynamic Testing)
   * Manual code review
   * Threat modelling
   * Dependency scanning





# Key Takeaways

SAST is powerful at detecting:

* Known dangerous APIs
* Obvious injection flows
* Misconfigurations
* Pattern-based weaknesses

SAST is weak at detecting:

* Business logic flaws
* Runtime-dependent vulnerabilities
* Complex multi-stage exploits
* Cross-service abuse
* Real-world exploit chains

The professional security tester understands:

> SAST finds code smells.
> Humans find real-world exploits.

Mastering security testing for Python means knowing not just how to run tools — but knowing where their vision ends.

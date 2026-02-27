---
title: Recognizing AI Coding Patterns 
short_title: Insecure AI Coding Patterns 
---


Today, a significant proportion of Python applications are partially — and sometimes entirely — generated using AI coding assistants.

For the security tester, this should immediately trigger heightened scrutiny. AI-generated code often:

* Prioritises functionality over security
* Lacks contextual threat awareness
* Omits defensive programming controls
* Uses outdated or overly generic patterns

AI output is not inherently insecure — but it is frequently **under-hardened**.

Understanding the common fingerprints of AI-generated Python code can help you identify areas that deserve deeper manual review.

---

## Why AI-Generated Code Deserves Extra Attention

Large language models generate code by predicting statistically likely patterns. They:

* Do not understand your deployment architecture
* Do not assess risk in a real threat model
* Cannot reason about trust boundaries
* Often default to the simplest working example

This results in code that “works” — but may not be secure, robust, or production-ready.



## Common AI Coding Patterns That Signal Risk

Below are recurring patterns frequently observed in AI-generated Python code that may introduce direct weaknesses.


### use of `assert`

Example:

```python
assert user.is_admin
```
:::{danger}
Assertions are primarily for debugging and development, NOT for production validation or error handling.
:::


* `assert` statements are removed when Python is run with optimisation (`-O` flag).
* They are intended for debugging, not enforcing security controls.
* Using `assert` for authentication or authorisation checks creates a bypass condition in production.


Security-relevant checks must use explicit condition handling and raise proper exceptions.


### `except Exception: pass`

Example:

```python
try:
    process_payment(data)
except Exception:
    pass
```

Why This Is Dangerous:

* Silences security-relevant errors
* Hides failed validation
* Masks exploitation attempts
* Breaks logging and monitoring

This pattern is extremely common in AI-generated code because it “prevents crashes”.

:::{danger}
Silent failure is often worse than visible failure.
:::


### Overuse of the `os` Module Instead of `pathlib`

Example:

```python
import os
file_path = os.path.join("uploads", filename)
```


While not inherently insecure, this pattern may indicate:

* Outdated coding style
* Lack of modern path handling
* Increased risk of path traversal if not validated correctly

Modern Python encourages the use of `pathlib.Path`, which provides:

* Clearer semantics
* Safer path resolution
* Easier normalisation

AI tools often default to older `os`-based patterns.

As a tester, you should carefully audit:

* File concatenation
* Path normalisation
* Directory traversal protections


### Absence of Modern Python (3.10+) Features

AI-generated code frequently avoids newer language features such as:

* Structural pattern matching (`match` / `case`)
* Improved type hinting
* `|` union types
* Dataclass enhancements
* Exception groups

While this is not a vulnerability in itself, it may indicate:

* The model was trained on older examples
* The codebase has not been modernised
* Security improvements available in newer versions are not leveraged

Outdated style can correlate with:

* Weak validation patterns
* Poor typing discipline
* Reduced clarity in control flow

All of which increase the likelihood of hidden weaknesses.


## Additional AI Red Flags

Experienced testers also report the following patterns in AI-produced Python code:

* Excessively verbose comments explaining trivial logic
* Copy-paste style structure across unrelated modules
* Missing authentication checks in example endpoints
* Hard-coded secrets in demonstration code
* Lack of input validation on public-facing functions

These patterns are not proof of AI usage — but they often correlate with it.


## The Security Tester’s Approach

When you suspect AI-generated code:

1. Increase scrutiny on input handling.
2. Audit exception handling rigorously.
3. Search for unsafe defaults.
4. Review authentication and authorisation boundaries manually.
5. Verify that security controls are explicit — not implied.

Remember:
:::{caution}
AI optimises for **“working code”**, not **“secure code”**.
:::


:::{warning}
AI-generated Python code is not automatically insecure — but it is frequently:

* Under-validated
* Over-permissive
* Poorly hardened
* Incompletely defensive
:::

A skilled Python security tester recognises the patterns, then performs deeper manual analysis where automated reasoning has likely fallen short.

:::{note}
In modern Python security testing, **recognising AI coding fingerprints** is becoming a core review skill.
:::

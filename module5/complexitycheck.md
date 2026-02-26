---
title: Cyclomatic Complexity Checks in Python Security Testing 
short_title: Complexity Check
---

## Overview 
When performing security testing on Python code, a **simple cyclomatic complexity check** is one of the fastest and most effective early risk indicators you can apply.

Complex code has a lot of disadvantages when it comes to managing security risks. Making corrections is difficult and errors are easily made.

**Python Code Audit** implements a Cyclomatic Complexity check, operating on the principle that secure systems are simple systems.




[Cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity) is a software metric used to indicate the complexity of a program. It was developed by Thomas J. McCabe, Sr. in 1976. 

Cyclomatic complexity measures the number of independent execution paths through a function or module. 

Calculating the cyclomatic complexity for Python source code is difficult to do accurately. Most implementations aiming for a thorough complexity score eventually become somewhat subjective or opinionated.



:::{note} 
**Python Code Audit** takes a pragmatic and simple approach to determine and calculate the complexity of a source file.

The Complexity Score that **Python Code Audit** presents gives a **good and solid** representation for the complexity of a Python source file.
:::



The complexity is determined per file, and not per function within a Python source file. I have worked with companies that calculated [function points](https://en.wikipedia.org/wiki/Function_point) for systems that needed to be created or adjusted. Truth is: Calculating exact metrics about complexity for software code projects is a lot of work, is seldom done correctly and are seldom used with nowadays devops or scrum development teams. 




## Importance for Security Auditing


Complexity directly impacts security. Simple systems are:

* Maintainable: Easier to change and manage.

* Reliable: Less prone to logic errors.

* Testable: Easier to validate and test.

**Python Code Audit** tool calculates the complexity per file and provides a module-level overview to help you track this metric.


High cyclomatic complexity is strongly correlated with security risk for several reasons:

1. **Hidden Logic Paths**
   The more branches a function has, the harder it becomes to reason about all possible execution paths. Security vulnerabilities often hide in rarely executed branches.

2. **Incomplete Testing Coverage**
   Each independent path ideally requires at least one test case. As complexity grows, full path coverage becomes impractical, increasing the chance that:

   * Authentication checks are bypassed
   * Error handling leaks sensitive data
   * Validation logic is skipped in edge cases

3. **Inconsistent Input Validation**
   Complex conditional structures frequently lead to inconsistent sanitization or validation across branches, creating injection or authorization flaws.

4. **Exception Handling Risks**
   Multiple `try/except` blocks can unintentionally swallow security-critical exceptions, masking failures in cryptographic checks, permission validation, or deserialization logic.

Cyclomatic complexity is an early-warning system. **Python Code Audit** makes it simple to automate this check and consistently highlight high-risk areas.

Python security testing involves analysing intricate execution paths where vulnerabilities—which often elude automated testing tools—can remain undetected.


:::{admonition} Security Mindset
:class: tip

Cyclomatic complexity is not just a maintainability metric — it is a **security signal**. Complex code increases cognitive load, and security flaws thrive where reasoning is difficult.

In security testing for Python, a simple complexity check is a low-cost, high-value control that helps you identify where deeper manual review is most needed.
:::

## How does Code Audit calculates the Complexity?

Every function, method, or script starts with a base complexity of 1 (i.e., one execution path with no branching).

It adds 1 for each control structure or branching point:
| **AST Node Type** | **Reason for Increasing Complexity** |
|---|---|
| If | Conditional branch (if/elif/else) |
| For, While | Loop constructs (create additional paths) |
| Try | Potential for exception handling (adds branch) |
| ExceptHandler | Each except adds a new error-handling path |
| With | Context manager entry/exit paths |
| BoolOp | and / or are logical branches |
| Match | Match statement (like switch in other langs) |
| MatchCase | Each case adds an alternative path |
| Assert | Introduces an exit point if the condition fails |


**Python Code Audit** calculates the cyclomatic complexity of Python code using Python’s built-in Python `ast` (Abstract Syntax Tree) module.

Example:
```Python
"""complexity of code below should count to 4
Complexity breakdown:
1 (base)


+1 (if)


+1 (and) operator inside if


+1 (elif) â€” counted as another If node in AST
 = 4


"""
def test(x):
    if x > 0 and x < 10:
        print("Single digit positive")
    elif x >= 10:
        print("Two digits or more")
    else:
        print("Non-positive")
```

You can verify the complexity of a single Python file with the command:
```bash
 codeaudit filescan <filename.py>
```

Summary:
* Python Code Audit only analyzes the top-level structure. It doesn't distinguish between functions on purpose, unless the input is separated accordingly.
* Python Code Audit uses a simplified cyclomatic complexity approach to get fast inside from a security perspective. This may differ from tools, especially since implementation choices that are made for dealing with comprehensions, nested functions will be different.

## Checking Python Code Complexity with Python Code Audit 

### Check complexity for a Package or local directory

To check the complexity of e.g. the requests package:

```Python
codeaudit overview requests
```

This gives:
* `Median_Complexity` : The median (middle) complexity score across all scanned files.
This provides a realistic baseline of the overall code complexity.
* `Maximum_Complexity` The highest complexity score found in a single file. This is particularly important from a security perspective, as it immediately highlights files that may require deeper inspection.

And per file security relevant statistics that are equal when running the command:
 
```Python
codeaudit filescan request
```

### Check complexity for a single local Python file

To analyze the complexity of a single Python file:


```bash
 codeaudit filescan <myfilename.py>
```
This command generates detailed security-relevant statistics for the file.


For every Python file the following **security** relevant statistics are determined:

* **Number Of Code Lines**: Too many Lines Of Code (LoC) means a higher risk. Large code bases require a lot of effort to keep the security risks manageable. A large number of LoCs (Lines Of Code) means extra effort for maintenance there is a severe risks that new features or fixes will introduce new security risks.

* **Number of AST_Nodes**: Codeaudit calculates the number or 'AST Nodes' based on creating an Abstract Syntax Tree (AST) of a file. This to give a solid insight in the complexity of Python source code. Code Audit does not simply counts nodes, but complexity is determined by an algorithm where e.g. the number of `if-else` loops is counted and weighted. More information about complexity can be found in the section [Codeaudit complexity Check](complexitycheck).

* **Number of Modules**: A high the number of used modules used within a Python file can mean more security risks. This since there are more dependencies to manage. To get more insight in modules used in a Python file you **SHOULD** use the `codeaudit modulescan` command!

* **Number of Functions**. There is no such thing as a perfect architecture for Python programs. However there are many programs that are simple **bad** designed. Too many functions in one Python file in combination with one of the other statistics is an indication for possible security risks.

* **Number of Classes**. 

* **Number of Comment_Lines**. Python files with too little or too many comment lines can have impact on maintenance from a security point of view. 

* **Complexity_Score**: Per file the complexity of file is determined. A high complexity score can in potential result in more possible security risks. 

* **Number of Warnings**: A normal Python source file should not give Warnings. Warnings should be solved to prevent security risks in future. 
# Pareto principle for Python Security

The OWASP Top 10 is an excellent example that shows that of all possible security weaknesses only a small percentage still leads to the majority of security breaches. The OWASP Top 10 project analyses CVEs (Common Vulnerabilities and Exposures) and calculates an impact score.

SAST testing for Python is a low-effort method with a very high success rate.

![pareto_for_python](/images/pareto.png)



:::{tip} 
Static application security testing (SAST) tools , like this [**Python Code Audit**](https://nocomplexity.com/codeaudit/) program **SHOULD BE** used to prevent security risks or be aware of potential risks that comes with running the software.
:::

In this course we will use the FOSS SAST tool for Python: [**Python Code Audit**](https://nocomplexity.com/codeaudit/):  
 
- [**Python Code Audit**](https://nocomplexity.com/codeaudit/) is designed for Python codebases. It is tailored to Python’s syntax and unique constructs, enabling it to identify potential security issues effectively.

- **Python Code Audit** SAST tool is an advanced security solution that automates the review of Python source code to identify potential security vulnerabilities.

- At a function level, Python Code Audit makes use of a common technique to scan the Python source files by making use of **'Abstract Syntax Tree(AST)'** to do in-depth checks on possible vulnerable constructs. 


:::{note} 
Simple good cyber security is possible by [Shift left](https://nocomplexity.com/documents/simplifysecurity/shiftleft.html). By detecting issues early in the SLDC process the cost to solve potential security issues is low. 

**Python SAST testing is a typical shift-left approach.**
:::

Most Python security defects can be traced back to:

1. Design mistakes

2. Weaknesses in the code. This also applies to AI-generated code, as many AI code generators do not produce secure code by default.

![sast_in_context](/images/sast_in_context.png)
---
title: Human in the loop
short_title: Human in the loop
---

You can and should automate security testing. Good test automation saves time and, if done well, increases the number of vulnerabilities identified.

However, SAST and other types of Python security testing still require human expertise.

It is highly recommended always to perform a SAST scan on Python code before using it. However, running a SAST scan on Python code does not constitute a complete security assessment. A comprehensive security assessment of Python code should also include:

- **Security architecture review:** Key questions include: What is the context? Who are the users? Which interfaces will be available? What other security measures are enabled by design within the environment? How are security principles applied (both in code and in processes)?

- Review of **relevant requirements** and user stories

- **Security design review**, with particular attention to design decisions that may impact security. A key question is: What implicit assumptions have been made during implementation?


The primary advantage of SAST for Python is automation. 

:::{important} 
SAST tools automatically scan the code’s structure, data flow, and control flow **without executing the code.** 
:::

![human-in-the-loop](/images/human_in_the_loop.png)
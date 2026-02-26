---
title: Isolation Techniques for Python security testing
short_title: Secure testing for Python
---

## Overview of Techniques

A secure test environment protects your system, your data, and ensures your Python programs behave reliably, while allowing safe experimentation and testing unknown Python programs.


:::{caution} 
A Python Virtual Environment (venv / virtualenv / conda-environment) **does not** isolate the system! 
Malicious Python code can still access your files, network, and OS.

However a Python virtual environment is still crucial for managing dependencies. Often a 'Python' environment is created within a secure sandbox (like a Virtual Machine, Container, BSDjail , etc)
:::

Common options for creating a secure test environment:

-  **Docker Containers (or Podman)** (isolated, reproducible environments)

+++

- **BSD Jails**:When using BSD, the simplest way to isolate programs is by using Jails. 
FreeBSD Jails enhance security by providing an OS-level virtualisation method that isolates processes, file systems, and network resources into separate, secure environments on a single kernel.

+++

- Use a **dedicated testing device (laptop or virtual server)** and delete the environment once testing is complete, for example by deleting the virtual machine or reinstalling the operating system. A common OS choice for security testing is Kali Linux.

+++

- [**gVisor**](https://gvisor.dev/). This is an User-space kernel / container sandbox. 
It provides **strong isolation for containers** by intercepting system calls and running them in user space instead of letting them touch the host kernel directly.
    - **Security:** High — much harder for malicious code in a container to escape to the host system compared to standard Docker.
    - **Use case:** Running untrusted code in containers, sandboxing microservices, or isolating test environments.
gVisor can be seen as a **“mini-kernel” inside your container** that acts as a safety layer between the app and the host OS.


+++

- [**Firecracker**](https://firecracker-microvm.github.io/):A Lightweight micro-VM (Virtual Machine). Firecracker is essentially **a very small, fast virtual machine**, optimized for security and performance, unlike full VMs which are heavier.
    - Designed to run thousands of isolated micro-VMs efficiently on a single host, originally for serverless platforms like AWS Lambda and Fargate.
    - Very high — each micro-VM has its **own kernel**, so even if code is malicious, it’s contained within the VM.





**Comparison:**

| Method                  | Purpose                     | Security Level                                   |
|-------------------------|----------------------------|------------------------------------------------|
| venv / Conda            | Dependency management       | None (System access is open)                  |
| PyPy / RestrictedPython | Software-level restriction  | Low (Hard to close all escape vectors)       |
| Docker /Podman / Containers     | OS-level virtualisation     | Medium (Better, but shares a kernel)         |
| BSDjail            | OS-level virtualisation     | High                  |
| gVisor / Firecracker    | Micro-VM / Sandboxing       | High (Strongest isolation)                    |


:::{tip} 
If you're testing running untrusted Python code , [Podman](https://podman.io/) is usually the safer default.
Setup is simpler!
:::

:::{admonition} Security Differences Between Docker and Podman
:class: tip, dropdown

| Feature              | Docker            | Podman             |
|----------------------|------------------|--------------------|
| Daemon required      | ✅ Yes            | ❌ No              |
| Rootless support     | Optional         | Native-first       |
| Attack surface       | Larger (daemon)  | Smaller            |
| Multi-user systems   | Needs care       | Safer by default   |

:::

## Practical Tip


If baseline system security hygiene is in place — for example, using separate user privileges for Python installations and avoiding system-wide package installation — then a Python virtual environment (such as `venv` or `conda`) is sufficient for routine security validation of Python libraries.

It should be noted, however, that a virtual environment provides dependency isolation rather than a security boundary. Any malicious code executed within the environment will still run with the privileges of the invoking user. For the analysis of untrusted or potentially malicious code, stronger isolation mechanisms — such as containerisation (e.g. Docker) or full virtual machines — are recommended.


:::{hint} 
For Static Application Security Testing (SAST) of Python code using [**Python Code Audit**](https://github.com/nocomplexity/codeaudit), security is important; however, **the Python code is not executed**.

This means that the required security level does not need to be the highest possible.

However, you should always be cautious about non-Python binaries that may be installed, as they might contain malware.
:::
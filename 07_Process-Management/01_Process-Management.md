### What is a Process?
--- 

- A process is defined as a running instance of a program on a Linux server.
- Examples include a Python application, shell script, or web server instance.
- Processes cannot directly interact with hardware resources (CPU, memory, disk); the operating system manages hardware resource allocation.

**Role of the Operating System**
---

- The OS handles CPU scheduling, memory management, file system management, and network management.
- When a process is CPU or memory intensive, it consumes a disproportionate share of resources, affecting other processes.

**CPU and Memory Intensive Processes**
---

- Example: A Python machine learning (ML) application performing heavy calculations will consume a large portion of CPU time.
- When CPU resources are monopolized (e.g., 90%), other processes (e.g., web server or cron jobs) receive minimal CPU time.
- Similarly, a Java application with many threads may consume 90% of available memory, leading to out of memory errors for other applications.

**Key Administrative Tasks in Process Management**
---

As a Linux administrator, three fundamental activities must be performed:

- **Viewing running processes** to understand what is active on the system.
- **Killing or stopping processes**  when they consume excessive resources or cause system instability.
- **Prioritizing or deprioritizing processes** to control CPU time allocation.

Administrators can adjust process priority using Linux commands to optimize system performance.

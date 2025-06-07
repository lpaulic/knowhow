---
layout: default
title: Overview 
parent: FreeRTOS
nav_order: 1
---

# Free RTOS Overview
{: .no_toc }

## RTOS Fundamentals

These notes are retrieved from freeRTOS: [page](https://www.freertos.org/Documentation/01-FreeRTOS-quick-start/01-Beginners-guide/01-RTOS-fundamentals).

In real time means that the system is time deterministic. Alongside the requirement that the logic
behaviour is correnct, the time in which the logic executes must be inside a constant 
narrow timeframe. A real time system is not necessary fast but is always consistent.

There are two categories of real time systems:
- hard real time -> deviations result in system failure (usless system)
- soft real time -> small deviations are allowed (deviations depend on the domain)

### Multitasking

Feature of operating systems where a kernel in the operating system can execute multiple tasks, where
a task (task) is a program in execution. Multi tasking OSs can symplify the application design in a way
that an application can be partitioned in small tasks. Tasks communicate to each other using the OS 
utilities. Tasks can be divided by multiple teams. Complex timing and sequnecing is delegated to the
OS. Multitasking is executing multiple tasks in sections, where only one task is running at one moment.
This gives the illusion that single processors can run tasks concurrently.

### Scheduling

The scheduler is part of the kernel and is responsible for which task should be executing at some point
in time. The scheduler can suspend and resume a task many times during the task lifetime.

Scheduling policy is the algorithm used by the scheduler to decide which task to execute at some point
in time. For non real time OS the scheduler will most likely allow each task a "fair" proportion of
processor time.

In addition to a task being involuntarily suspended by the kernel, a task can choose to suspend itself.
It will do this by either delaying (sleep) for a fixed period, or wait (block) for a resource to become
available or an event to occur. A blocked or sleeping task is not able to execute and will not allocate
any process time.

### Context switching

As a task executes it utilizes the processor / microcontroller registers and accesses RAM and ROM just 
as any other program. These resources together (the processor registers, stack, etc.) comprise the 
task execution context. 

The operating system kernel is responsible for ensuring that a task can resume it execution from the last
point it was active. All the resources should be restored and to the task it should appear as nothing
happened. The process of storing the active context before switching tasks and restoring a context
is known as context switching.

### Links and resources
1. [FreeRTOS book 1.1 (FreeRTOS V10.6.2)](https://github.com/FreeRTOS/FreeRTOS-Kernel-Book/releases/download/V1.1.0/Mastering-the-FreeRTOS-Real-Time-Kernel.v1.1.0.pdf)

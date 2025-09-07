# Task Planning in a Datacenter

**Author:** Mihai-Emilian Băban (334CD)

## Overview

This project focuses on the efficient scheduling of tasks across multiple hosts in a datacenter environment. The core component, `MyDispatcher`, is responsible for assigning tasks to hosts based on various scheduling algorithms. Each host executes assigned tasks according to their own queue management and priority rules.

## Scheduling Algorithms Implemented

### 1. Round Robin
- Tasks are allocated to hosts in a cyclic manner: `(i + 1) % n`, where `i` is the ID of the last host that received a task and `n` is the total number of hosts.

### 2. Shortest Queue
- The dispatcher scans all hosts and selects the host with the shortest queue.
- If a task is currently executing, its duration is included in the queue size calculation.
- The new task is then assigned to that host.

### 3. Size Interval Task Assignment
- Tasks are assigned based on their size:
    - **Short Tasks** → Host 0
    - **Medium Tasks** → Host 1
    - **Long Tasks** → Host 2

### 4. Least Work Left
- Similar to Shortest Queue, but selects the host with the lowest total remaining computation time (including running and queued tasks).

## Host Responsibilities (`MyHost`)
- Handles execution of tasks.
- Uses a custom `QueueComparator` for priority queue management. If two tasks have the same priority, they are compared by start time.
- `getWorkLeft()` computes the total remaining duration of all queued tasks plus the remaining time of the currently running task.
- Executes the highest priority task from the queue and marks it as running.
- During execution, if the running task is preemptible and a higher priority task arrives, the higher priority task is executed immediately and the preempted task is returned to the queue.
- Tasks are marked as complete once their remaining time reaches zero.

## How It Works

1. Tasks are submitted to the dispatcher.
2. The dispatcher assigns tasks to hosts according to the selected scheduling algorithm.
3. Hosts manage their own task queues and execute tasks based on priority and preemption rules.


## Difference between Binary Semaphore  VS Counting Semaphore

Let’s see some common difference between binary  and counting semaphore:

|   |   |
|---|---|
|**Binary Semaphore**|**Counting Semaphore**|
|Mutual exclusion|No mutual exclusion|
|Semaphore Value is only 0 and 1|Semaphore Value is any integer value|
|The only process at the same time.|Can provide a set of Processes|
|Only one slot|More than one slot|

## Advantages of Semaphores

Some of the advantages of semaphores are mentioned below:

- Semaphores strictly follow the principle of **mutual exclusion** and allow only one process into the critical section at the same time.
- Semaphores are **machine-independent**, so Semaphores are implemented in the machine-independent code of the microkernel.
- Semaphores allow flexible [management of resources](https://t4tutorials.com/resource-allocation-graph-resource-instance-management-and-advantages/).
- Semaphores can be considered as **more efficient** than other methods of synchronization.

## Disadvantages of Semaphores

Some of the disadvantages of semaphores are mentioned below;

- Semaphores are very complex to implement, so the wait and signal operations must be implemented in the correct order. If the wait and signal operations are not implemented in the correct order, then it can be a cause of a deadlock.
- Semaphores can be lead to priority inversion.  In priority inversion, [low priority processes](https://t4tutorials.com/priority-based-process-scheduling-in-operating-systems/) may win the critical section and access first, and high priority processes get the critical section after the low priority process.
- The operating system needs to do some extra work and maintains track of all calls to wait and signal operations in semaphore.
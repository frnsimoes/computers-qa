Found a great resource on namespaces[^1]. Especially the Part 2, namespeaces API. 

What is a namespace?

> A namespace wraps a global system resource in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the resource. Namespaces are used for a variety of purposes, with the most notable being the implementation of containers, a technique for lightweight virtualization. ([source](https://lwn.net/Articles/531381/))

Essentially, the namespace API has three parts: `clone`, `unshare`, and `setns`.

- `clone` is the new version of the `fork` syscall[^3]. The difference is that with `clone` with can use flags to control aspects of the new process. For example: `CLONE_NEWNS` creates the process with a new mount namespace. Check all flags masks [here].
- `setns` is a syscall that let's us add process to an existing namespace.
- `unshare` operates on the calling process (e.g., by executing on the shell `unshare --flag run /bin/bash`), where `--flag` is the equivalent of `clone`'s `NEW_*`. Try, for example, executing `unshare` `--fork`, `--mount-proc` and `--pid`.

[^1]: https://lwn.net/Articles/766124/
[^2]: https://lwn.net/Articles/531381/
[^3]: From The Linux Programming Interface: Like fork() and vfork(), the Linux-specific clone() system call creates a new process. It differs from the other two calls in allowing finer control over the steps that occur during process creation. 
[here]: https://man7.org/linux/man-pages/man2/clone.2.html

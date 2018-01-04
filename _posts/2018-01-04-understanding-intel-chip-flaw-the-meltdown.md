---
layout: post
title: "Intel Chip Flaw, the Meltdown"
description: "Detail understanding the Meltdown - flaw with the processor from Intel"
categories: [security]
tags: [tutorial,security]
---

## Short background

### What is Kernel

Kernel is the core of all OS. It's a piece of program that acts like God in the cloud for all other applications to pray to, ask for. Kernel is the gatekeeper for files accessing, memory management, device management, and other system calls. Kernel itself keeps the references of all other processes in memory, and its address ranges are protected from standard user access.

This separating and protecting from regular access called memory isolation, which modern computer relies on to provide fundamental security to each process.

### Meltdown

Meltdown is a type of attack that exploits out-of-order execution (OOOE) to read kernel memory locations. This means all secrets held or cached by Kernel, such as credential of other programs, or even the operating system, are exposed to normal program execution. This attack does not rely on any software vulnerabilities and can be exploited in any operating system, which is extra dangerous.

On the cloud computing term, where many users may use a single computer, Meltdown may be exploited to read other user credentials and secrets as well. It meltdown all boundaries created by software to isolate application.

## Meltdown for dummy

A detail description of Meltdown is locate [here](https://googleprojectzero.blogspot.jp/2018/01/reading-privileged-memory-with-side.html). In this post, I'm going to summarize the method so a beginner can understand.

A Meltdown attack consists of 3 steps:

1. Reading the secret.
2. Transmitting the secret.
3. Rebuild the secret.

### Reading the secret

Hacker loads a memory location, which is initially inaccessible into a medium, is the best choice is a register for speed and resilient. To read the secret, the hacker takes advantage of OOOE to realize this.

Consider the most simple sample in pseudo code like this

{% highlight javascript linenos=table %}
    raise Error()
    process(probe[data * 2<<12])
{% endhighlight %}

The second line, in theory, should not be executed. But in reality,  to improve speed, the processor performs it transiently and then ignore the outcome. This is so-called out-of-order execution, one of technique to increase speed implement by Intel processors.

The results of this out-of-order execution will be trashed, and the contents handled by them will be wiped out as well, resulting register and memory changes are never committed. However, the cache memory contents are still kept in place.

Let consider a bit detail example of pseudo code above:

{% highlight nasm linenos=table %}
; rbx = kernel_address
; rcx = probe_address
; read the kernel_address, exception will be raise because the action is prohibited
mov al, byte [rbx]
; Multiple with the cache page size
shl rax, 0xc
; Intentionally spacing through the cache table
mov rcx, qword [rcx + rax]
{% endhighlight %}

At line number 4, a series of operations are already got thrown in the execution queue, including line 6 and 8. Line 4 raises an exception, and the registers and memory eventually get wiped at the end of the queue, the data in cache table still exists.

### Transmitting the secret

What we are talking about the data is still in cache even after the `mov` instruction in line 4 retired. In fact, the cache is not the only one method to transmit information obtained by OOOE to the hacker. Meltdown uses `Flush+Reload` to build a fast and reliable channel transmitting the secret back.

Assuming one cache page has the size of 4KB. Attacker allocates a probe array in the memory of 256 x 4KB, and ensure that no part of it is cached. To transmit the data, we consider the most simple case, to send 1 byte of 256 states.

The OOOE adds multiplied secret data with the base address of the probe array, intentionally caching the corresponding cache page. With 256 cache pages made with spatial distance to avoid loading adjacent memory locations into the cache, the hacker can determine 256 states of the byte.

After retrieving the secret, described in the next step, the whole process is repeated on next byte, until we read all inaccessible memory.

### Rebuild the secret

Meltdown attack relies on [Flush+Reload](https://www.usenix.org/system/files/conference/usenixsecurity14/sec14-paper-yarom.pdf) to transfer the secret data back to the hacker. After all OOOE sequences are executed, only one cache page of the probe array is cached; the attacker can iterate through all 256 pages of the probe array to find corresponding data.

## For further reading

[Anders Fogh's blog post](https://cyber.wtf/2017/07/28/negative-result-reading-kernel-memory-from-user-mode/)
---
title: About Linux Capabilities 
author: Watskip
date: 2020-10-06 18:55:00 -0400
categories: [Nix]
tags: [Capabilities]
pin: false
---
# About Linux Capabilities

Linux capabilities are not known to most of those who don't program with the Linux Kernel but checking Capabilities on certain binaries can help us on escalating privileges.

## What about them?

On a Linux system there are 2 kinds of processes:

- Privileged processes :: Processes with an euid of *0* (*root*)
- Unprivileged processes :: Processes with an euid that is not *0*

Capabilities provide us to independently divide the permissions of the root user on a specific binary. An unprivileged process that is provided with capabilities can bypass kernel permission checks depending on the capability that it has been assigned to it.

There are multiple capabilities but some of them are:

- CAP_DAC_OVERRIDE :: We can use this capability to bypass file read, write, and execute permission checks.
- CAP_DAC_READ_SEARCH :: This capability can help us bypass file/directory read checks.
- CAP_KILL :: Send arbitrary signals to processes
- CAP_SETGID :: Manipulate and forge GIDs
- CAP_SETUID :: Manipulate and forge UIDs

## What can we do with them?

From a defensive perspective, capabilities has the power to restrict to a specific process or binary a privilege from the superuser. This means if the process or binary is compromised then the potential damage is limited compared to having a process or binary running with an euid of the superuser.

But in the same way, a process with a single capability can still be abused to escalate privileges.

This is meant to reveal the feature of capabilities to those that didn't knew them. Next you can find some more references to learn more about the topic.

### Further References

[https://www.insecure.ws/linux/getcap_setcap.html](https://www.insecure.ws/linux/getcap_setcap.html)

[https://www.vultr.com/docs/working-with-linux-capabilities](https://www.vultr.com/docs/working-with-linux-capabilities)

[https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099](https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)

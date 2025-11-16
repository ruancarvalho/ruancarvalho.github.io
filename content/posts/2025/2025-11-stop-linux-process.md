---
title: "How to Identify and Stop Linux Processes"
date: 2025-11-15T11:00:00+00:00
tags: ["linux", "homelab"]
categories: ["Homelab"]
draft: false
url: "/posts/stop-linux-process/"
---

I wrote this guide for me to remember how to identify and stop processes using standard commands for Linux distributions. I use it mostly for my Homelab.

## Understanding Process Termination

Linux identifies every running program with a *Process ID* (PID).  
To stop a process, you typically send a signal:

- **SIGINT (interrupt)** — sent by pressing `Ctrl + C`  
- **SIGTERM (terminate)** — graceful shutdown (`kill <PID>`)  
- **SIGKILL** — forceful termination (`kill -9 <PID>`)  

---

## Stopping Background Processes

If a process was started with "&", or placed in the background, or detached from the terminal, you must stop it by identifying its PID.

### 1. Locate the PID using `ps`

```bash
ps aux | grep <process-name>
```

Example:

```bash
ps aux | grep python
```

### 2. Stop the process gracefully

```bash
kill <PID>
```

This issues SIGTERM.

### 3. Force termination (if required)

If the process does not respond:

```bash
kill -9 <PID>
```

This sends SIGKILL, which immediately removes the process without cleanup.

---

## Finding Processes with pgrep

`pgrep` provides a concise way to locate a process:

```bash
pgrep -a <name>
```

This displays the PID and command line.
Example:

```bash
pgrep -a yt-dlp
```

This works for any application or script.

---

## Stopping Processes Started by Scripts, Cron, or nohup

Background jobs launched indirectly (cron, shell scripts, automation tools) will not appear in terminal history. To identify them:

```bash
pgrep -a <name>
```

or:

```bash
ps -ef | grep <name>
```

Then terminate normally:

```bash
kill <PID>
```

If required:

```bash
kill -9 <PID>
```

---

## Verifying That a Process Has Been Terminated

To confirm:

```bash
pgrep -a <name>
```

If there is no output, the process is no longer running.

---

## Summary

| Task                                 | Command or Action             |
| ------------------------------------ | ----------------------------- |
| Interrupt running foreground process | `Ctrl + C`                    |
| Find process by name                 | `pgrep -a <name>`             |
| Gracefully stop a process            | `kill <PID>`                  |
| Forcefully stop a process            | `kill -9 <PID>`               |
| List all processes                   | `ps aux`                      |
| Inspect processes interactively      | `top` or `htop`               |
| Apply execution timeout              | `timeout <seconds> <command>` |
| Confirm process termination          | `pgrep -a <name>`             |

That's it.

I usually need these commands when I do something wrong with scripts in my Homelab.

This guide has the core tools required to control and terminate processes in Linux, whether they are command-line utilities, long-running scripts, or background applications.



# Linux Architecture, Processes, and systemd

## Quick Linux Architecture View

```text
Applications
    ↓
User Space
    ↓
Kernel
    ↓
Hardware
```

---

## Linux Kernel
- Core part of Linux
- Talks directly to hardware
- Handles:
  - CPU
  - Memory
  - Storage
  - Networking
  - Processes

Think of the kernel as the middle layer between software and hardware.

---

## User Space
- Where normal programs run
- Example programs:
  - bash
  - nginx
  - python
  - docker
- Cannot directly access hardware

Programs send requests to the kernel to perform tasks.

---

## init / systemd
- First process started when Linux boots
- PID = 1
- Starts and manages system services

### systemd responsibilities
- Starts services automatically
- Restarts failed services
- Manages boot process
- Collects logs
- Controls background services

Examples:
- ssh
- nginx
- docker

---

## How Processes Are Created and Managed
- Every running program becomes a process
- Processes are created mainly using `fork()`
- Parent process creates child process
- Kernel manages:
  - PID (Process ID)
  - Memory
  - CPU scheduling
  - Permissions

Linux is constantly managing processes in the background.

---

## Common Linux Process States

| State | Meaning |
|---|---|
| Running | Currently using CPU |
| Sleeping | Waiting for input or resource |
| Stopped | Paused process |
| Zombie | Finished process waiting for cleanup |

Zombie processes are dead processes whose parent has not cleaned them yet.

---

## Daily Linux Commands

| Command | Purpose |
|---|---|
| `ps` | Show running processes |
| `top` | Live system/process monitoring |
| `htop` | Better interactive process viewer |
| `systemctl` | Manage systemd services |
| `journalctl` | View system logs |

### Example Usage

```bash
ps aux
top
htop
systemctl status nginx
journalctl -u docker
```

---

## Why systemd Is Important
- Used in most modern Linux distributions
- Makes service management easier
- Automatically handles failed services
- Simplifies server operations and troubleshooting

Without systemd, managing servers manually becomes difficult.

---

## Why This Matters for DevOps
- Servers depend on processes and services
- Troubleshooting often means checking logs and running processes
- Docker, Kubernetes, CI/CD tools, and monitoring tools rely on Linux process management
- systemd knowledge helps with:
  - EC2 troubleshooting
  - Service failures
  - Automation
  - Production server management

Basic Linux understanding is the foundation of DevOps work.

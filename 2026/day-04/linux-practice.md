# linux-practice.md

# Day 04 - Linux Fundamentals Practice

## Goal

Practice basic Linux troubleshooting and system inspection commands.

---

# Process Checks

## 1. Check Running Processes

Command:

```bash
ps -ef | head
```

Output:

```bash
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 10:10 ?        00:00:01 /sbin/init
root         512       1  0 10:10 ?        00:00:00 sshd
ubuntu       890     850  0 10:15 pts/0    00:00:00 bash
ubuntu      1045     890  0 10:20 pts/0    00:00:00 ps -ef
```

Observation:

* Verified active system processes
* PID helps identify processes

---

## 2. Check Process Using `top`

Command:

```bash
top
```

Observation:

* CPU and memory usage visible
* System load average displayed
* Helpful for troubleshooting high resource usage

---

## 3. Search Specific Process

Command:

```bash
pgrep sshd
```

Output:

```bash
512
```

Observation:

* Confirmed SSH service process is running

---

# Service Checks

## 4. Check SSH Service Status

Command:

```bash
systemctl status ssh
```

Output:

```bash
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded
     Active: active (running)
```

Observation:

* SSH service is active and running properly

---

## 5. List Running Services

Command:

```bash
systemctl list-units --type=service --state=running
```

Observation:

* Displayed active running services
* Useful for checking service availability

---

# Log Checks

## 6. View SSH Logs

Command:

```bash
journalctl -u ssh --no-pager | tail -n 10
```

Output:

```bash
Accepted password for ubuntu
Started OpenBSD Secure Shell server
```

Observation:

* Verified SSH login activity
* Logs help in troubleshooting authentication issues

---

## 7. View System Logs

Command:

```bash
tail -n 20 /var/log/syslog
```

Observation:

* Checked recent system log entries
* Useful for identifying errors and warnings

---

# Mini Troubleshooting Steps

## Scenario:

Verify whether SSH service is running correctly.

Steps Performed:

### Step 1 - Check Service Status

```bash
systemctl status ssh
```

Result:

* Service was active

---

### Step 2 - Verify Process

```bash
pgrep sshd
```

Result:

* SSH process found

---

### Step 3 - Check Logs

```bash
journalctl -u ssh --no-pager | tail
```

Result:

* No critical errors found

---

# Commands Practiced Today

| Command              | Purpose                  |
| -------------------- | ------------------------ |
| ps -ef               | View running processes   |
| top                  | Monitor system resources |
| pgrep                | Find process PID         |
| systemctl status     | Check service status     |
| systemctl list-units | List running services    |
| journalctl           | View service logs        |
| tail                 | Read latest logs         |

---

# What I Learned

* How to inspect running processes
* How to verify system services
* How to read logs for troubleshooting
* Basic Linux troubleshooting workflow

---

# Why This Matters for DevOps

Linux troubleshooting is part of daily DevOps work.

These commands help with:

* Debugging production servers
* Investigating service failures
* Monitoring system health
* Understanding Linux environments

Consistent practice improves troubleshooting speed and confidence.

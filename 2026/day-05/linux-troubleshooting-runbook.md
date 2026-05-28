# linux-troubleshooting-runbook.md

# Day 05 - Linux Troubleshooting Runbook

## Target Service

Service inspected: `ssh.service`

Goal:
Perform a quick Linux troubleshooting drill using system snapshots, logs, and service inspection.

---

# 1. Environment Basics

## Check Kernel and System Info

Command:

```bash
uname -a
```

Output:

```bash
Linux ubuntu 6.8.0-31-generic x86_64 GNU/Linux
```

Observation:

* Verified Linux kernel version and architecture
* System is running Ubuntu Linux

---

## Check OS Release

Command:

```bash
cat /etc/os-release
```

Output:

```bash
NAME="Ubuntu"
VERSION="24.04 LTS"
```

Observation:

* Confirmed operating system version
* Helpful during package or compatibility troubleshooting

---

# 2. Filesystem Sanity Checks

## Create Temporary Troubleshooting Folder

Command:

```bash
mkdir /tmp/runbook-demo
```

Observation:

* Created temporary working directory successfully

---

## Copy and Verify File

Command:

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

Output:

```bash
-rw-r--r-- 1 root root 250 hosts-copy
```

Observation:

* File operations working correctly
* Verified read/write access

---

# 3. Snapshot: CPU & Memory

## Check Running Processes

Command:

```bash
top
```

Observation:

* CPU usage stable
* No abnormal spikes observed
* Load average low

---

## Check Memory Usage

Command:

```bash
free -h
```

Output:

```bash
Mem: 3.8Gi used 1.1Gi free 1.9Gi
```

Observation:

* Memory usage within safe range
* No swap pressure detected

---

## Inspect SSH Process Resource Usage

Command:

```bash
ps -o pid,pcpu,pmem,comm -p $(pgrep sshd | head -1)
```

Output:

```bash
PID %CPU %MEM COMMAND
512  0.0  0.1 sshd
```

Observation:

* SSH process consuming minimal resources
* No CPU or memory concern

---

# 4. Snapshot: Disk & IO

## Check Disk Usage

Command:

```bash
df -h
```

Output:

```bash
/dev/root  30G   12G   17G  42%
```

Observation:

* Disk usage healthy
* Enough free space available

---

## Check Log Directory Size

Command:

```bash
du -sh /var/log
```

Output:

```bash
180M /var/log
```

Observation:

* Log directory size reasonable
* No unusual log growth

---

## Check System IO Statistics

Command:

```bash
vmstat 1 3
```

Observation:

* No high IO wait observed
* System responsiveness normal

---

# 5. Snapshot: Network

## Check Listening Ports

Command:

```bash
ss -tulpn
```

Output:

```bash
tcp LISTEN 0 128 0.0.0.0:22
```

Observation:

* SSH service listening on port 22
* Network socket active

---

## Test Network Connectivity

Command:

```bash
curl -I https://google.com
```

Output:

```bash
HTTP/2 200
```

Observation:

* Outbound internet connectivity working
* DNS resolution successful

---

# 6. Logs Reviewed

## Review SSH Service Logs

Command:

```bash
journalctl -u ssh -n 20 --no-pager
```

Output:

```bash
Started OpenBSD Secure Shell server
Accepted password for ubuntu
```

Observation:

* SSH service started normally
* Successful login entries visible

---

## Review System Logs

Command:

```bash
tail -n 20 /var/log/syslog
```

Observation:

* No critical errors found
* System logs appear clean

---

# 7. Quick Findings

* SSH service is healthy and running
* CPU and memory usage stable
* Disk usage normal
* Network connectivity functional
* No recent critical log errors detected

---

# 8. If This Worsens

## Next Steps

### 1. Restart SSH Service Carefully

```bash
sudo systemctl restart ssh
```

Purpose:

* Recover service if connections start failing

---

### 2. Increase Log Monitoring

Command:

```bash
journalctl -u ssh -f
```

Purpose:

* Watch live logs during issue reproduction

---

### 3. Collect Deeper Diagnostics

Commands:

```bash
strace -p <PID>
```

```bash
ss -tulpn
```

Purpose:

* Trace system calls
* Inspect network connection problems

---

# Commands Practiced

| Command             | Purpose               |
| ------------------- | --------------------- |
| uname -a            | System information    |
| cat /etc/os-release | OS details            |
| mkdir               | Create directory      |
| cp                  | Copy files            |
| top                 | Monitor CPU/memory    |
| free -h             | Check RAM usage       |
| ps                  | Inspect process usage |
| df -h               | Check disk space      |
| du -sh              | Check directory size  |
| vmstat              | System statistics     |
| ss -tulpn           | Check listening ports |
| curl -I             | Test connectivity     |
| journalctl          | View service logs     |
| tail                | Read latest logs      |

---

# Why This Matters for DevOps

This troubleshooting drill helps build:

* Fast incident response habits
* Confidence reading Linux signals
* Log-first debugging mindset
* Better production troubleshooting skills

Small repeatable checks reduce downtime and avoid guesswork during real incidents.

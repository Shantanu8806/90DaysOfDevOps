# day-07-linux-fs-and-scenarios.md

# Day 07 - Linux File System Hierarchy & Scenario-Based Practice

## Part 1: Linux File System Hierarchy

### `/` (Root Directory)

Purpose:

* The starting point of the Linux file system.
* Every file and directory exists under `/`.

Command:

```bash
ls -l /
```

Observed:

* `home`
* `etc`
* `var`

I would use this when:

* Navigating the overall Linux file system structure.

---

### `/home`

Purpose:

* Contains home directories for regular users.

Command:

```bash
ls -l /home
```

Observed:

* `ubuntu`
* `devops`

I would use this when:

* Accessing user files, scripts, and project directories.

---

### `/root`

Purpose:

* Home directory for the root user.

Command:

```bash
sudo ls -l /root
```

Observed:

* `.bashrc`
* `.profile`

I would use this when:

* Working with administrative files and root-owned scripts.

---

### `/etc`

Purpose:

* Stores system-wide configuration files.

Command:

```bash
ls -l /etc | head
```

Observed:

* `hostname`
* `hosts`

I would use this when:

* Troubleshooting configuration issues.

---

### `/var/log`

Purpose:

* Contains application and system logs.

Command:

```bash
ls -l /var/log | head
```

Observed:

* `syslog`
* `auth.log`

I would use this when:

* Investigating errors and service failures.

---

### `/tmp`

Purpose:

* Temporary storage used by applications and users.

Command:

```bash
ls -l /tmp | head
```

Observed:

* Temporary files
* Application runtime files

I would use this when:

* Creating temporary test files during troubleshooting.

---

### `/bin`

Purpose:

* Contains essential Linux commands.

Command:

```bash
ls -l /bin | head
```

Observed:

* `cat`
* `ls`

I would use this when:

* Running core Linux commands.

---

### `/usr/bin`

Purpose:

* Contains most user-level command binaries.

Command:

```bash
ls -l /usr/bin | head
```

Observed:

* `vim`
* `grep`

I would use this when:

* Running commonly installed utilities.

---

### `/opt`

Purpose:

* Stores optional or third-party applications.

Command:

```bash
ls -l /opt
```

Observed:

* Application-specific directories

I would use this when:

* Managing manually installed software.

---

## Hands-On Tasks

### Find Largest Log Files

Command:

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

Observation:

* Identified the largest log directories and files.

---

### View Hostname Configuration

Command:

```bash
cat /etc/hostname
```

Observation:

* Displayed current server hostname.

---

### Check Home Directory

Command:

```bash
ls -la ~
```

Observation:

* Listed hidden files and user configuration files.

---

# Part 2: Scenario-Based Practice

## Scenario 1: Service Not Starting

Problem:
A service named `myapp` failed after reboot.

### Step 1

Command:

```bash
systemctl status myapp
```

Why:

* Checks if service is running, stopped, or failed.

---

### Step 2

Command:

```bash
journalctl -u myapp -n 50
```

Why:

* Reviews recent service logs.

---

### Step 3

Command:

```bash
systemctl is-enabled myapp
```

Why:

* Verifies if service starts automatically during boot.

---

### Step 4

Command:

```bash
systemctl list-units --type=service
```

Why:

* Confirms service exists and checks related services.

---

### What I Learned

Always check status first, then logs, then boot configuration.

---

## Scenario 2: High CPU Usage

Problem:
Application server feels slow.

### Step 1

Command:

```bash
top
```

Why:

* Displays live CPU usage.

---

### Step 2

Command:

```bash
ps aux --sort=-%cpu | head -10
```

Why:

* Lists highest CPU-consuming processes.

---

### Step 3

Command:

```bash
pgrep <process_name>
```

Why:

* Finds the PID of the process.

---

### Step 4

Command:

```bash
ps -p <PID> -o pid,ppid,%cpu,%mem,cmd
```

Why:

* Displays detailed process information.

---

### What I Learned

Identify the process first before taking action.

---

## Scenario 3: Finding Service Logs

Problem:
Developer asks for Docker service logs.

### Step 1

Command:

```bash
systemctl status docker
```

Why:

* Verifies service state.

---

### Step 2

Command:

```bash
journalctl -u docker -n 50
```

Why:

* Displays last 50 log entries.

---

### Step 3

Command:

```bash
journalctl -u docker -f
```

Why:

* Follows logs in real time.

---

### What I Learned

Systemd-managed services store logs in journald.

---

## Scenario 4: File Permission Issue

Problem:
`backup.sh` returns "Permission denied".

### Step 1

Command:

```bash
ls -l /home/user/backup.sh
```

Why:

* Checks current permissions.

---

### Step 2

Command:

```bash
chmod +x /home/user/backup.sh
```

Why:

* Adds execute permission.

---

### Step 3

Command:

```bash
ls -l /home/user/backup.sh
```

Why:

* Verifies permission changes.

---

### Step 4

Command:

```bash
./backup.sh
```

Why:

* Tests script execution.

---

### What I Learned

Scripts require execute permissions (`x`) to run.

---

# Key Takeaways

* `/etc` contains configurations.
* `/var/log` is the first place to look during troubleshooting.
* `journalctl` is essential for service logs.
* `top` and `ps` help identify resource issues.
* `chmod +x` fixes common script execution problems.
* Understanding the Linux file system improves troubleshooting speed.

---

# Why This Matters for DevOps

These directories and troubleshooting flows are used daily in:

* Production support
* Cloud servers
* CI/CD environments
* Container platforms
* Incident response

Learning where files live and how to investigate problems quickly is a core DevOps skill.

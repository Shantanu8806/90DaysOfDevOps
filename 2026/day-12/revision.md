# Day 12 – Revision & Reflection (Days 01–11)

## Objective

Review the Linux and cloud fundamentals covered during the first 11 days of the challenge and reinforce the concepts through small hands-on exercises.

---

# 1. Learning Plan Review

### Original Goal

* Learn Linux fundamentals
* Build confidence with cloud servers
* Understand permissions, users, groups, and troubleshooting
* Develop habits used in real DevOps environments

### Current Progress

* Comfortable navigating Linux systems
* Able to connect to cloud servers using SSH
* Understand basic troubleshooting workflow
* Familiar with file permissions and ownership management

### Adjustment for Upcoming Days

* Spend more time on shell scripting
* Improve troubleshooting speed
* Practice Docker and cloud deployments more frequently

---

# 2. Process & Service Checks

## Command 1

```bash
ps aux | head
```

Observation:

* Displayed running processes and system services.
* Confirmed multiple background processes are active.

---

## Command 2

```bash
systemctl status nginx
```

Observation:

* Nginx service is active and running.
* Service is enabled and starts automatically on boot.

---

## Command 3

```bash
journalctl -u nginx -n 20
```

Observation:

* Recent requests were recorded successfully.
* No critical errors found in the latest logs.

---

# 3. File Skills Practice

## Append Text

```bash
echo "Day 12 revision practice" >> notes.txt
```

Observation:

* Successfully added content to an existing file.

---

## Check Permissions

```bash
ls -l notes.txt
```

Observation:

* Verified current ownership and permissions.

---

## Modify Permissions

```bash
chmod 640 notes.txt
```

Observation:

* Owner has read/write access.
* Group has read access.
* Others have no access.

---

# 4. Cheat Sheet Refresh

## Five Commands I Would Use First During an Incident

### 1. ps aux

Why:

* Quickly identifies running processes.

---

### 2. top

Why:

* Displays real-time CPU and memory usage.

---

### 3. systemctl status

Why:

* Checks whether a service is healthy.

---

### 4. journalctl

Why:

* Reviews service logs for failures and warnings.

---

### 5. df -h

Why:

* Checks disk usage and identifies storage issues.

---

# 5. User & Group Sanity Check

## Verify Existing User

```bash
id tokyo
```

Observation:

* Confirmed user exists and belongs to expected groups.

---

## Verify Ownership

```bash
ls -l devops-file.txt
```

Observation:

* Ownership changes from Day 11 are still correctly applied.

---

# Mini Self-Check

## 1. Which 3 commands save you the most time right now, and why?

### ps aux

* Quickly shows running processes.

### systemctl status

* Provides immediate service health information.

### journalctl -u <service>

* Helps identify service failures without searching through multiple log files.

---

## 2. How do you check if a service is healthy?

Commands I would run:

```bash
systemctl status nginx
```

```bash
journalctl -u nginx -n 20
```

```bash
ps aux | grep nginx
```

Reason:

* Confirms service status, recent logs, and running processes.

---

## 3. How do you safely change ownership and permissions without breaking access?

Example:

```bash
sudo chown ubuntu:developers app.log
chmod 640 app.log
```

Explanation:

* First assign correct ownership.
* Then grant only the permissions required.

---

## 4. What will you focus on improving in the next 3 days?

* Linux shell scripting
* Docker fundamentals
* Faster troubleshooting workflows
* Better understanding of networking concepts

---

# Key Takeaways From Days 01–11

* Linux commands become easier through repetition.
* Logs are usually the first place to investigate issues.
* Correct permissions and ownership are essential for security.
* Service troubleshooting follows a predictable workflow:

  * Check status
  * Review logs
  * Verify resources
* Cloud servers are simply Linux systems accessed remotely.

---

# Commands Reviewed Today

```bash
ps aux | head

systemctl status nginx

journalctl -u nginx -n 20

echo "Day 12 revision practice" >> notes.txt

chmod 640 notes.txt

id tokyo

ls -l devops-file.txt
```

---

# Conclusion

The first 11 days established a solid foundation in Linux administration, troubleshooting, cloud server management, file permissions, users, groups, and ownership. The next phase will focus on automation, scripting, containers, and more advanced DevOps practices.

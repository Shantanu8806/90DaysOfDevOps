# Day 08 - Cloud Server Setup: Docker, Nginx & Web Deployment

## Objective

Deploy a web server on a cloud VM, configure network access, verify web accessibility, and collect logs.

---

# Cloud Instance Details

| Item           | Value            |
| -------------- | ---------------- |
| Cloud Provider | AWS EC2          |
| OS             | Ubuntu 24.04 LTS |
| Instance Type  | t2.micro         |
| Region         | eu-north-1       |
| Web Server     | Nginx            |
| Public IP      | <YOUR_PUBLIC_IP> |

---

# Part 1: SSH Access

## Connect to Instance

Command:

```bash
ssh -i my-key.pem ubuntu@<YOUR_PUBLIC_IP>
```

Output:

```bash
ubuntu@ip-172-31-x-x:~$
```

Observation:

* Successfully connected to EC2 instance.
* Verified SSH access using key pair authentication.

---

# Part 2: Install Docker

## Update Packages

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Install Docker

```bash
sudo apt install docker.io -y
```

Verify Installation:

```bash
docker --version
```

Example Output:

```bash
Docker version 28.x.x
```

---

## Check Docker Service

```bash
sudo systemctl status docker
```

Observation:

* Docker service active and running.

---

# Part 3: Install Nginx

## Install Nginx

```bash
sudo apt install nginx -y
```

---

## Verify Nginx Status

```bash
sudo systemctl status nginx
```

Output:

```bash
Active: active (running)
```

---

## Enable Nginx on Boot

```bash
sudo systemctl enable nginx
```

---

# Part 4: Security Group Configuration

Inbound Rules Added:

| Type | Protocol | Port |
| ---- | -------- | ---- |
| SSH  | TCP      | 22   |
| HTTP | TCP      | 80   |

---

## Verify Web Access

Browser URL:

```text
http://<YOUR_PUBLIC_IP>
```

Result:

* Nginx Welcome Page displayed successfully.

Screenshot:

```text
nginx-webpage.png
```

---

# Part 5: Extract Nginx Logs

## View Access Logs

```bash
sudo tail -n 20 /var/log/nginx/access.log
```

Observation:

* Browser requests visible in access logs.

---

## View Error Logs

```bash
sudo tail -n 20 /var/log/nginx/error.log
```

Observation:

* No critical errors found.

---

## Save Logs to File

```bash
sudo cat /var/log/nginx/access.log > ~/nginx-logs.txt
```

Verify:

```bash
cat nginx-logs.txt
```

---

## Download Log File

From local machine:

```bash
scp -i my-key.pem ubuntu@<YOUR_PUBLIC_IP>:~/nginx-logs.txt .
```

Downloaded File:

```text
nginx-logs.txt
```

---

# Commands Used

```bash
ssh -i my-key.pem ubuntu@<IP>

sudo apt update
sudo apt upgrade -y

sudo apt install docker.io -y
docker --version

sudo apt install nginx -y

sudo systemctl status docker
sudo systemctl status nginx

sudo systemctl enable nginx

sudo tail -n 20 /var/log/nginx/access.log
sudo tail -n 20 /var/log/nginx/error.log

sudo cat /var/log/nginx/access.log > ~/nginx-logs.txt

scp -i my-key.pem ubuntu@<IP>:~/nginx-logs.txt .
```

---

# Challenges Faced

### Issue 1: Website Not Opening

Cause:

* Port 80 was not allowed in Security Group.

Fix:

* Added inbound HTTP rule (TCP 80).

---

### Issue 2: Permission Error While Downloading Logs

Cause:

* Incorrect file ownership or path.

Fix:

* Copied log file to home directory before downloading.

---

# What I Learned

* How to launch and access an EC2 instance.
* How to install and manage Docker and Nginx.
* How Security Groups control network access.
* How to verify service status using systemctl.
* How to collect and download log files from a remote server.

---

# Screenshots Submitted

```text
ssh-connection.png
nginx-webpage.png
docker-nginx.png
```

---

# Files Submitted

```text
day-08-cloud-deployment.md
nginx-logs.txt
```

---

# Why This Matters for DevOps

This exercise introduced real-world DevOps workflows:

* Cloud server provisioning
* Remote administration with SSH
* Service installation and management
* Firewall and security group configuration
* Log collection and troubleshooting

These skills are fundamental for managing production infrastructure.

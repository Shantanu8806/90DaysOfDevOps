# linux-commands-cheatsheet.md

# Linux Commands Practice for DevOps Beginners

> Quick handwritten-style Linux notes for daily DevOps practice

---

# 1. Process Management

## `ps`

Shows running processes

```bash
ps -ef
```

---

## `top`

Live CPU and memory monitoring

```bash
top
```

---

## `htop`

Better interactive process monitor

```bash
htop
```

---

## `kill`

Stops process using PID

```bash
kill 1234
```

Force kill:

```bash
kill -9 1234
```

---

## `pkill`

Kills process using process name

```bash
pkill nginx
```

---

## `pgrep`

Finds process PID

```bash
pgrep docker
```

---

## `jobs`

Shows background jobs

```bash
jobs
```

---

## `bg`

Runs stopped process in background

```bash
bg
```

---

## `fg`

Brings process to foreground

```bash
fg
```

---

## `nohup`

Runs process after logout

```bash
nohup python app.py &
```

---

# 2. File System & Navigation

## `pwd`

Shows current directory

```bash
pwd
```

---

## `ls`

Lists files and folders

```bash
ls -lah
```

---

## `cd`

Changes directory

```bash
cd /var/log
```

---

## `mkdir`

Creates directory

```bash
mkdir project
```

---

## `touch`

Creates empty file

```bash
touch notes.txt
```

---

## `cp`

Copies files/folders

```bash
cp app.conf backup/
```

---

## `mv`

Moves or renames files

```bash
mv old.txt new.txt
```

---

## `rm`

Deletes files/folders

```bash
rm -rf temp/
```

---

## `find`

Searches files/directories

```bash
find / -name nginx.conf
```

---

## `grep`

Searches text inside files

```bash
grep "error" app.log
```

---

## `cat`

Displays file content

```bash
cat config.yaml
```

---

## `less`

Reads large files safely

```bash
less /var/log/syslog
```

---

## `head`

Shows first lines of file

```bash
head -20 app.log
```

---

## `tail`

Shows last lines of file

```bash
tail -f app.log
```

---

## `chmod`

Changes file permissions

```bash
chmod 755 deploy.sh
```

Memory trick:

* 7 = rwx
* 5 = r-x

---

## `chown`

Changes ownership

```bash
sudo chown ubuntu:ubuntu app.log
```

---

## `df -h`

Checks disk usage

```bash
df -h
```

---

## `du -sh`

Shows folder size

```bash
du -sh logs/
```

---

## `tar`

Archives files

```bash
tar -czvf backup.tar.gz project/
```

---

## `zip`

Compresses files

```bash
zip logs.zip *.log
```

---

# 3. Networking & Troubleshooting

## `ping`

Checks connectivity

```bash
ping google.com
```

---

## `ip addr`

Shows IP addresses

```bash
ip addr
```

---

## `curl`

Tests APIs and websites

```bash
curl http://example.com
```

---

## `wget`

Downloads files

```bash
wget https://example.com/file.zip
```

---

## `dig`

DNS lookup tool

```bash
dig google.com
```

---

## `nslookup`

Checks DNS resolution

```bash
nslookup github.com
```

---

## `netstat`

Shows listening ports

```bash
netstat -tulnp
```

---

## `ss`

Modern netstat replacement

```bash
ss -tulnp
```

---

## `traceroute`

Tracks network path

```bash
traceroute google.com
```

---

## `host`

Checks domain IP

```bash
host openai.com
```

---

## `ssh`

Remote server login

```bash
ssh ubuntu@10.0.0.10
```

---

## `scp`

Secure file transfer

```bash
scp file.txt ubuntu@server:/home/ubuntu/
```

---

# 4. Logs & Monitoring

## `journalctl`

Views system logs

```bash
journalctl -u nginx
```

---

## `free -h`

Checks memory usage

```bash
free -h
```

---

## `uptime`

Shows uptime and load

```bash
uptime
```

---

## `vmstat`

CPU and memory statistics

```bash
vmstat
```

---

## `iostat`

Checks disk I/O

```bash
iostat
```

---

## `watch`

Runs command repeatedly

```bash
watch df -h
```

---

## `dmesg`

Kernel boot/system logs

```bash
dmesg | tail
```

---

## `history`

Shows command history

```bash
history
```

---

## `crontab`

Schedules recurring tasks

```bash
crontab -e
```

Example:

```bash
*/5 * * * * /home/ubuntu/script.sh
```

Runs every 5 minutes.

---

# 5. User & Permissions

## `whoami`

Shows current user

```bash
whoami
```

---

## `id`

Shows UID and groups

```bash
id
```

---

## `sudo`

Runs command as admin

```bash
sudo apt update
```

---

## `passwd`

Changes password

```bash
passwd
```

---

## `useradd`

Creates new user

```bash
sudo useradd devops
```

---

## `usermod`

Modifies user groups/settings

```bash
sudo usermod -aG docker ubuntu
```

---

# 6. Package Management

## `apt`

Ubuntu package manager

```bash
sudo apt update
sudo apt install nginx
```

---

## `yum`

RHEL/CentOS package manager

```bash
sudo yum install httpd
```

---

## `snap`

Installs snap packages

```bash
sudo snap install code --classic
```

---

# 7. Docker Related Commands

## `docker ps`

Shows running containers

```bash
docker ps
```

---

## `docker logs`

Shows container logs

```bash
docker logs container_id
```

---

## `docker exec`

Access running container

```bash
docker exec -it container_id bash
```

---

# 8. Quick DevOps Revision Notes

* `tail -f` → live logs
* `grep` → search logs quickly
* `curl` → API testing
* `ssh` → remote server access
* `df -h` → storage usage
* `free -h` → memory usage
* `top` → CPU monitoring
* `journalctl` → service logs
* `chmod 755` → executable permissions

---

# Common Real DevOps Tasks

## Check CPU Usage

```bash
top
```

---

## Check Memory Usage

```bash
free -h
```

---

## Watch Logs Live

```bash
tail -f /var/log/syslog
```

---

## Check Open Ports

```bash
ss -tulnp
```

---

## Restart Service

```bash
sudo systemctl restart nginx
```

---

## Check Service Status

```bash
systemctl status nginx
```

---

# Why This Matters for DevOps

Linux powers:

* Cloud servers
* Docker containers
* Kubernetes clusters
* CI/CD pipelines
* Monitoring systems
* Production infrastructure

These commands help you:

* Troubleshoot faster
* Debug production issues
* Understand servers better
* Automate tasks confidently
* Work efficiently in terminal

---

# Final Tip

Best way to learn Linux:

1. Practice daily
2. Use commands manually
3. Read logs often
4. Break things safely
5. Build small projects

> Linux becomes easy with repetition, not memorization.

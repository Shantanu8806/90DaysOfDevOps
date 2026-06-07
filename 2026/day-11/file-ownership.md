# Day 11 - File Ownership Challenge (chown & chgrp)

## Objective

Learn how Linux file ownership works and practice changing owners and groups using `chown` and `chgrp`.

---

# Task 1: Understanding Ownership

## Check Ownership in Home Directory

Command:

```bash
ls -l
```

Sample Output:

```text
-rw-r--r-- 1 ubuntu ubuntu 0 Jun 11 10:00 notes.txt
-rw-r--r-- 1 ubuntu ubuntu 0 Jun 11 10:05 script.sh
```

### Ownership Format

```text
-rw-r--r-- 1 owner group size date filename
```

### Difference Between Owner and Group

* **Owner**: The user who owns the file.
* **Group**: A collection of users who may share access to the file.

---

# Task 2: Basic chown Operations

## Create File

```bash
touch devops-file.txt
```

Check Current Ownership:

```bash
ls -l devops-file.txt
```

Example:

```text
-rw-r--r-- 1 ubuntu ubuntu 0 Jun 11 10:15 devops-file.txt
```

---

## Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

Verify:

```bash
ls -l devops-file.txt
```

Output:

```text
-rw-r--r-- 1 tokyo ubuntu 0 Jun 11 10:15 devops-file.txt
```

---

## Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

Verify:

```bash
ls -l devops-file.txt
```

Output:

```text
-rw-r--r-- 1 berlin ubuntu 0 Jun 11 10:15 devops-file.txt
```

---

# Task 3: Basic chgrp Operations

## Create File

```bash
touch team-notes.txt
```

Check Current Group:

```bash
ls -l team-notes.txt
```

---

## Create Group

```bash
sudo groupadd heist-team
```

---

## Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

Verify:

```bash
ls -l team-notes.txt
```

Output:

```text
-rw-r--r-- 1 ubuntu heist-team 0 Jun 11 10:20 team-notes.txt
```

---

# Task 4: Combined Owner & Group Change

## Create Configuration File

```bash
touch project-config.yaml
```

Change Owner and Group Together:

```bash
sudo chown professor:heist-team project-config.yaml
```

Verify:

```bash
ls -l project-config.yaml
```

Output:

```text
-rw-r--r-- 1 professor heist-team 0 Jun 11 10:25 project-config.yaml
```

---

## Create Directory

```bash
mkdir app-logs
```

Change Ownership:

```bash
sudo chown berlin:heist-team app-logs
```

Verify:

```bash
ls -ld app-logs
```

Output:

```text
drwxr-xr-x 2 berlin heist-team 4096 Jun 11 10:30 app-logs
```

---

# Task 5: Recursive Ownership

## Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

---

## Create Group

```bash
sudo groupadd planners
```

---

## Change Ownership Recursively

```bash
sudo chown -R professor:planners heist-project
```

Verify:

```bash
ls -lR heist-project
```

Sample Output:

```text
heist-project/
├── plans
└── vault

plans/strategy.conf
vault/gold.txt
```

Observation:

* All files and folders now belong to `professor:planners`.

---

# Task 6: Practice Challenge

## Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

---

## Create Directory

```bash
mkdir bank-heist
```

---

## Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

---

## Assign Ownership

### access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

### blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

### escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

---

## Verify

```bash
ls -l bank-heist
```

Example Output:

```text
-rw-r--r-- 1 tokyo   vault-team 0 access-codes.txt
-rw-r--r-- 1 berlin  tech-team  0 blueprints.pdf
-rw-r--r-- 1 nairobi vault-team 0 escape-plan.txt
```

---

# Files & Directories Created

### Files

* devops-file.txt
* team-notes.txt
* project-config.yaml
* heist-project/vault/gold.txt
* heist-project/plans/strategy.conf
* bank-heist/access-codes.txt
* bank-heist/blueprints.pdf
* bank-heist/escape-plan.txt

### Directories

* app-logs
* heist-project
* bank-heist

---

# Ownership Changes

| File/Directory      | Before        | After                |
| ------------------- | ------------- | -------------------- |
| devops-file.txt     | ubuntu:ubuntu | berlin:ubuntu        |
| team-notes.txt      | ubuntu:ubuntu | ubuntu:heist-team    |
| project-config.yaml | ubuntu:ubuntu | professor:heist-team |
| app-logs            | ubuntu:ubuntu | berlin:heist-team    |
| heist-project       | ubuntu:ubuntu | professor:planners   |
| access-codes.txt    | ubuntu:ubuntu | tokyo:vault-team     |
| blueprints.pdf      | ubuntu:ubuntu | berlin:tech-team     |
| escape-plan.txt     | ubuntu:ubuntu | nairobi:vault-team   |

---

# Commands Used

```bash
ls -l
ls -ld
ls -lR

touch
mkdir

chown
chown -R

chgrp

groupadd
useradd
```

---

# What I Learned

1. Every Linux file has both an owner and a group.
2. `chown` can change owner and group together.
3. `chgrp` changes only the group ownership.
4. Recursive ownership changes are useful for entire projects.
5. Proper ownership is critical for applications, logs, and shared directories.


---

# Conclusion

Successfully practiced file ownership management using `chown`, `chgrp`, and recursive ownership changes. Verified ownership assignments for files, directories, and project structures.

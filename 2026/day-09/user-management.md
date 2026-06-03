# Day 09 - Linux User & Group Management Challenge

## Objective

Practice Linux user management, group management, permissions, and shared workspace configuration.

---

# Task 1: Create Users

## Create Users

Commands:

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
```

## Set Passwords

```bash
sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
```

## Verification

Check users in passwd file:

```bash
grep -E "tokyo|berlin|professor" /etc/passwd
```

Check home directories:

```bash
ls -l /home
```

Observed:

```text
tokyo
berlin
professor
```

---

# Task 2: Create Groups

## Create Groups

```bash
sudo groupadd developers
sudo groupadd admins
```

## Verification

```bash
grep -E "developers|admins" /etc/group
```

Observed:

```text
developers
admins
```

---

# Task 3: Assign Users to Groups

## Add Users

```bash
sudo usermod -aG developers tokyo

sudo usermod -aG developers berlin
sudo usermod -aG admins berlin

sudo usermod -aG admins professor
```

## Verify Membership

```bash
groups tokyo
groups berlin
groups professor
```

Example Output:

```text
tokyo : tokyo developers

berlin : berlin developers admins

professor : professor admins
```

---

# Task 4: Shared Directory

## Create Directory

```bash
sudo mkdir -p /opt/dev-project
```

## Set Group Ownership

```bash
sudo chgrp developers /opt/dev-project
```

## Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

## Verify

```bash
ls -ld /opt/dev-project
```

Expected:

```text
drwxrwxr-x
```

---

## Test File Creation

As tokyo:

```bash
sudo -u tokyo touch /opt/dev-project/tokyo-file.txt
```

As berlin:

```bash
sudo -u berlin touch /opt/dev-project/berlin-file.txt
```

Verify:

```bash
ls -l /opt/dev-project
```

Observed:

```text
tokyo-file.txt
berlin-file.txt
```

---

# Task 5: Team Workspace

## Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

---

## Create Group

```bash
sudo groupadd project-team
```

---

## Add Users to Group

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

---

## Create Workspace Directory

```bash
sudo mkdir -p /opt/team-workspace
```

---

## Assign Group Ownership

```bash
sudo chgrp project-team /opt/team-workspace
```

---

## Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

---

## Verify

```bash
ls -ld /opt/team-workspace
```

Expected:

```text
drwxrwxr-x
```

---

## Test File Creation

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi-test.txt
```

Verify:

```bash
ls -l /opt/team-workspace
```

Observed:

```text
nairobi-test.txt
```

---

# Users & Groups Created

## Users

* tokyo
* berlin
* professor
* nairobi

## Groups

* developers
* admins
* project-team

---

# Group Assignments

| User      | Groups                   |
| --------- | ------------------------ |
| tokyo     | developers, project-team |
| berlin    | developers, admins       |
| professor | admins                   |
| nairobi   | project-team             |

---

# Directories Created

| Directory           | Group        | Permissions |
| ------------------- | ------------ | ----------- |
| /opt/dev-project    | developers   | 775         |
| /opt/team-workspace | project-team | 775         |

---

# Commands Used

```bash
useradd
passwd
groupadd
usermod
groups
mkdir
chgrp
chmod
ls
touch
```

---

# What I Learned

1. Users and groups help manage access securely.
2. Shared directories can be controlled through group ownership.
3. Linux permissions determine who can read, write, and execute files.
4. The `usermod -aG` command is used to add users to supplementary groups.
5. Group-based access management is commonly used in DevOps environments.

---

# Screenshots Added

* user-creation.png
* group-membership.png
* dev-project-permissions.png
* team-workspace-test.png

---

# Conclusion

Successfully created users, groups, shared directories, and verified access through Linux permissions and group assignments.

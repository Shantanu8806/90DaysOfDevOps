# Day 10 - File Permissions & File Operations Challenge

## Objective

Learn how to create, read, and manage files while understanding Linux file permissions.

---

# Task 1: Create Files

## Create Empty File

Command:

```bash
touch devops.txt
```

Verify:

```bash
ls -l devops.txt
```

---

## Create notes.txt with Content

Command:

```bash
echo "Linux file operations practice" > notes.txt
echo "Learning permissions and ownership" >> notes.txt
```

Verify:

```bash
cat notes.txt
```

Output:

```text
Linux file operations practice
Learning permissions and ownership
```

---

## Create script.sh

Command:

```bash
vim script.sh
```

Content:

```bash
echo "Hello DevOps"
```

Verify:

```bash
ls -l script.sh
```

---

# Task 2: Read Files

## Read notes.txt

Command:

```bash
cat notes.txt
```

Observation:

* Displayed complete file contents.

---

## View script.sh in Read-Only Mode

Command:

```bash
vim -R script.sh
```

Observation:

* File opened in read-only mode.

---

## Display First 5 Lines of /etc/passwd

Command:

```bash
head -n 5 /etc/passwd
```

Sample Output:

```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

---

## Display Last 5 Lines of /etc/passwd

Command:

```bash
tail -n 5 /etc/passwd
```

Observation:

* Displayed the last five user entries.

---

# Task 3: Understand Permissions

## Check File Permissions

Command:

```bash
ls -l devops.txt notes.txt script.sh
```

Example Output:

```text
-rw-r--r-- 1 ubuntu ubuntu 0 Jun 10 10:00 devops.txt
-rw-r--r-- 1 ubuntu ubuntu 60 Jun 10 10:05 notes.txt
-rw-r--r-- 1 ubuntu ubuntu 19 Jun 10 10:10 script.sh
```

### Understanding Permissions

| Permission | Meaning     |
| ---------- | ----------- |
| r          | Read (4)    |
| w          | Write (2)   |
| x          | Execute (1) |

For `-rw-r--r--`:

* Owner → Read + Write
* Group → Read
* Others → Read
* No execute permission

---

# Task 4: Modify Permissions

## Make script.sh Executable

Command:

```bash
chmod +x script.sh
```

Verify:

```bash
ls -l script.sh
```

Output:

```text
-rwxr-xr-x
```

Run Script:

```bash
./script.sh
```

Output:

```text
Hello DevOps
```

---

## Make devops.txt Read-Only

Command:

```bash
chmod a-w devops.txt
```

Verify:

```bash
ls -l devops.txt
```

Output:

```text
-r--r--r--
```

---

## Set notes.txt to 640

Command:

```bash
chmod 640 notes.txt
```

Verify:

```bash
ls -l notes.txt
```

Output:

```text
-rw-r-----
```

Meaning:

* Owner → Read + Write
* Group → Read
* Others → No access

---

## Create Directory with 755 Permissions

Command:

```bash
mkdir project
chmod 755 project
```

Verify:

```bash
ls -ld project
```

Output:

```text
drwxr-xr-x
```

---

# Task 5: Test Permissions

## Try Writing to Read-Only File

Command:

```bash
echo "new text" >> devops.txt
```

Result:

```text
Permission denied
```

Observation:

* Write operation failed because write permissions were removed.

---

## Try Executing a Non-Executable File

Remove execute permission:

```bash
chmod -x script.sh
```

Run:

```bash
./script.sh
```

Result:

```text
Permission denied
```

Observation:

* Linux requires execute permission to run scripts.

---

# Files Created

* devops.txt
* notes.txt
* script.sh
* project/

---

# Permission Changes

| File/Directory | Before     | After      |
| -------------- | ---------- | ---------- |
| script.sh      | -rw-r--r-- | -rwxr-xr-x |
| devops.txt     | -rw-r--r-- | -r--r--r-- |
| notes.txt      | -rw-r--r-- | -rw-r----- |
| project        | default    | drwxr-xr-x |

---

# Commands Used

```bash
touch
echo
cat
vim
vim -R
head
tail
ls -l
chmod +x
chmod a-w
chmod 640
chmod 755
mkdir
```

---

# What I Learned

1. Linux permissions control who can read, write, and execute files.
2. Scripts require execute (`x`) permission before they can run.
3. `chmod` can be used to assign permissions numerically or symbolically.
4. `head` and `tail` are useful for viewing large files quickly.
5. Proper permissions are important for system security and collaboration.

---

# Screenshots Added

* file-creation.png
* permissions-before-after.png
* script-execution.png
* project-directory-permissions.png

---

# Conclusion

Successfully created files, read file contents, modified permissions, tested access restrictions, and learned how Linux file permissions work in practice.

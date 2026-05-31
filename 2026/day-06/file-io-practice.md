# file-io-practice.md

# Day 06 - Linux Fundamentals: Read and Write Text Files

## Objective

Practice basic file creation, writing, appending, and reading using Linux commands.

---

## 1. Create File

Command:

```bash
touch notes.txt
```

Observation:

* Created an empty file named `notes.txt`.

---

## 2. Write Initial Content

Command:

```bash
echo "Day 06 Linux Practice" > notes.txt
echo "Learning file operations" >> notes.txt
echo "Using redirection operators" >> notes.txt
```

Observation:

* First command created content.
* `>>` appended new lines without overwriting.

---

## 3. Append Using tee

Command:

```bash
echo "Writing with tee command" | tee -a notes.txt
```

Output:

```text
Writing with tee command
```

Observation:

* Displayed text on screen and appended it to the file.

---

## 4. Add More Lines

Command:

```bash
echo "Reading files with cat" >> notes.txt
echo "Reading first lines with head" >> notes.txt
echo "Reading last lines with tail" >> notes.txt
echo "Linux files are easy to manage" >> notes.txt
```

---

## 5. Read Entire File

Command:

```bash
cat notes.txt
```

Output:

```text
Day 06 Linux Practice
Learning file operations
Using redirection operators
Writing with tee command
Reading files with cat
Reading first lines with head
Reading last lines with tail
Linux files are easy to manage
```

Observation:

* Displayed all file contents.

---

## 6. Read First Two Lines

Command:

```bash
head -n 2 notes.txt
```

Output:

```text
Day 06 Linux Practice
Learning file operations
```

Observation:

* Displayed only the beginning of the file.

---

## 7. Read Last Two Lines

Command:

```bash
tail -n 2 notes.txt
```

Output:

```text
Reading last lines with tail
Linux files are easy to manage
```

Observation:

* Displayed only the last two lines.

---

## Commands Practiced

| Command | Purpose                 |
| ------- | ----------------------- |
| touch   | Create file             |
| >       | Write/overwrite file    |
| >>      | Append content          |
| tee -a  | Display and append text |
| cat     | Read entire file        |
| head    | Read first lines        |
| tail    | Read last lines         |

---

## What I Learned

* How to create a text file
* Difference between `>` and `>>`
* How `tee` writes and displays output
* How to read full and partial file contents
* Basic file operations used daily in Linux and DevOps

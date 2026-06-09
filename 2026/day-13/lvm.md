# Objective 

Learn how Linux Logical Volume Manager (LVM) works and how it provides flexible storage management compared to traditional disk partitioning.

In this exercise, I practiced:

* Creating a Physical Volume (PV)
* Creating a Volume Group (VG)
* Creating a Logical Volume (LV)
* Formatting and mounting a logical volume
* Extending storage without recreating partitions

---

# What is LVM?

LVM (Logical Volume Manager) is a storage management layer that sits between physical disks and file systems.

Traditional partitions are fixed in size and difficult to resize later.

LVM solves this problem by allowing:

* Dynamic storage allocation
* Online volume expansion
* Easier disk management
* Storage pooling across multiple disks

---

# Why LVM is Important in DevOps

In production environments, applications often outgrow their storage.

Without LVM:

* Repartitioning disks can be risky.
* Downtime may be required.

With LVM:

* Storage can be expanded easily.
* Multiple disks can be combined.
* Disk management becomes more flexible.

Common examples:

* Database servers
* Application log storage
* Container host storage
* Cloud virtual machines

---

# LVM Architecture

LVM consists of three layers:

```text
Physical Disk
      ↓
Physical Volume (PV)
      ↓
Volume Group (VG)
      ↓
Logical Volume (LV)
      ↓
Filesystem
      ↓
Mount Point
```

Example:

```text
/dev/sdb
    ↓
PV
    ↓
devops-vg
    ↓
app-data
    ↓
ext4
    ↓
/mnt/app-data
```

---

# LVM Components

## Physical Volume (PV)

A Physical Volume is a disk or partition initialized for use by LVM.

Examples:

```bash
/dev/sdb
/dev/sdc
/dev/loop0
```

Physical Volumes provide the raw storage used by LVM.

---

## Volume Group (VG)

A Volume Group combines one or more Physical Volumes into a storage pool.

Example:

```text
PV1 + PV2 + PV3
        ↓
    devops-vg
```

Advantages:

* Storage can be expanded by adding more disks.
* Applications do not need to know how many disks exist underneath.

---

## Logical Volume (LV)

Logical Volumes are created from Volume Groups.

They function like traditional partitions.

Example:

```text
devops-vg
      ↓
app-data
```

Logical Volumes can be:

* Mounted
* Formatted
* Resized

---

# Environment Setup

Since no spare disk was available, a virtual disk was created.

## Create Virtual Disk

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
```

Explanation:

* Creates a 1GB file.
* File acts as a virtual disk.

---

## Attach Loop Device

```bash
losetup -fP /tmp/disk1.img
```

Explanation:

Associates the image file with a loop device.

Example:

```text
/dev/loop0
```

---

## Verify Loop Device

```bash
losetup -a
```

Output Example:

```text
/dev/loop0: []: (/tmp/disk1.img)
```

---

# Task 1 – Check Current Storage

## List Block Devices

```bash
lsblk
```

Purpose:

Displays:

* Disks
* Partitions
* Mount points

Sample Output:

```text
NAME      SIZE TYPE
sda        20G disk
└─sda1     20G part
loop0       1G loop
```

---

## Check Physical Volumes

```bash
pvs
```

Purpose:

Displays all Physical Volumes.

Initially:

```text
No PVs found
```

---

## Check Volume Groups

```bash
vgs
```

Purpose:

Displays Volume Groups.

Initially:

```text
No VGs found
```

---

## Check Logical Volumes

```bash
lvs
```

Purpose:

Displays existing Logical Volumes.

Initially:

```text
No LVs found
```

---

## Check Mounted Filesystems

```bash
df -h
```

Purpose:

Displays filesystem usage.

Important fields:

* Filesystem
* Size
* Used
* Available
* Mount Point

---

# Task 2 – Create Physical Volume

## Create PV

```bash
pvcreate /dev/loop0
```

Output:

```text
Physical volume "/dev/loop0" successfully created.
```

---

## Verify PV

```bash
pvs
```

Example:

```text
PV         VG   Fmt Attr PSize PFree
/dev/loop0      lvm2 ---  1.00g 1.00g
```

Observation:

* 1GB storage available.
* No Volume Group assigned yet.

---

# Task 3 – Create Volume Group

## Create VG

```bash
vgcreate devops-vg /dev/loop0
```

Output:

```text
Volume group "devops-vg" successfully created.
```

---

## Verify VG

```bash
vgs
```

Example:

```text
VG         #PV #LV #SN Attr   VSize VFree
devops-vg    1   0   0 wz--n- 1.00g 1.00g
```

Observation:

* VG created successfully.
* Entire disk capacity available.

---

# Task 4 – Create Logical Volume

## Create LV

```bash
lvcreate -L 500M -n app-data devops-vg
```

Explanation:

```text
-L 500M = size
-n app-data = LV name
```

Output:

```text
Logical volume "app-data" created.
```

---

## Verify LV

```bash
lvs
```

Example:

```text
LV        VG         Attr       LSize
app-data  devops-vg  -wi-a----- 500M
```

Observation:

* Logical Volume created successfully.
* Ready for formatting.

---

# Task 5 – Format and Mount

## Create Filesystem

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

Purpose:

Creates an ext4 filesystem.

---

## Create Mount Directory

```bash
mkdir -p /mnt/app-data
```

Purpose:

Creates mount point.

---

## Mount Volume

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

Purpose:

Makes filesystem accessible.

---

## Verify Mount

```bash
df -h /mnt/app-data
```

Example:

```text
Filesystem                     Size Used Avail Mounted on
/dev/mapper/devops--vg-appdata 488M  24M  439M /mnt/app-data
```

Observation:

Logical Volume successfully mounted.

---

# Task 6 – Extend the Volume

One of the biggest advantages of LVM is resizing storage without recreating partitions.

---

## Extend Logical Volume

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

Explanation:

Adds:

```text
200 MB
```

to existing volume.

---

## Resize Filesystem

```bash
resize2fs /dev/devops-vg/app-data
```

Purpose:

Allows ext4 filesystem to use newly allocated space.

---

## Verify Expansion

```bash
df -h /mnt/app-data
```

Example:

Before:

```text
488M
```

After:

```text
688M
```

Observation:

Storage expanded successfully without data loss.

---

# Real Production Example

Suppose an application stores logs in:

```text
/var/log/myapp
```

The application suddenly begins generating large log files.

Disk usage reaches:

```text
95%
```

Without LVM:

* Repartitioning required
* Possible downtime

With LVM:

```bash
lvextend -L +10G /dev/prod-vg/log-volume
resize2fs /dev/prod-vg/log-volume
```

Storage increases immediately.

---

# Key Commands Used

```bash
lsblk

pvs
vgs
lvs

pvcreate /dev/loop0

vgcreate devops-vg /dev/loop0

lvcreate -L 500M -n app-data devops-vg

mkfs.ext4 /dev/devops-vg/app-data

mkdir -p /mnt/app-data

mount /dev/devops-vg/app-data /mnt/app-data

df -h

lvextend -L +200M /dev/devops-vg/app-data

resize2fs /dev/devops-vg/app-data
```

---

# What I Learned

## 1. LVM Provides Flexible Storage Management

Unlike traditional partitions, Logical Volumes can be resized easily.

---

## 2. Storage is Organized into Layers

LVM uses:

```text
Physical Volume
      ↓
Volume Group
      ↓
Logical Volume
```

This abstraction simplifies disk management.

---

## 3. Volumes Can Be Expanded Without Recreating Partitions

Additional storage can be added quickly using:

```bash
lvextend
resize2fs
```

without affecting application data.

---

# Advantages of LVM

* Flexible storage allocation
* Easy volume expansion
* Storage pooling
* Better resource utilization
* Reduced downtime
* Supports snapshots
* Useful for cloud servers and production workloads

---

# Conclusion

LVM is a powerful storage management technology used extensively in Linux environments. It provides flexibility that traditional partitioning cannot offer. Through this exercise, I learned how to create Physical Volumes, Volume Groups, and Logical Volumes, mount filesystems, and dynamically expand storage when needed. These are essential skills for Linux administrators and DevOps engineers managing production infrastructure.

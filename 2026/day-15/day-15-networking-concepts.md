# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

# Introduction

Networking is one of the foundational skills for DevOps engineers. Every application deployed in the cloud depends on networking to communicate with users, databases, APIs, monitoring systems, and other services.

When troubleshooting application issues, many problems can be traced back to DNS resolution failures, incorrect IP addressing, subnet misconfigurations, firewall restrictions, or closed ports.

Understanding how these components work together helps DevOps engineers diagnose problems faster and build reliable systems.

---

# Task 1 – DNS: How Names Become IP Addresses

## What Happens When You Type google.com in a Browser?

When a user enters **google.com** into a browser, several networking processes occur behind the scenes:

1. The browser checks its local DNS cache.
2. The operating system checks its DNS cache.
3. If no cached entry exists, a DNS query is sent to a DNS resolver.
4. The DNS server returns the IP address associated with google.com.
5. The browser establishes a connection to that IP address.
6. The web page is requested and returned to the user.

Without DNS, users would need to remember IP addresses instead of domain names.

Example:

```text
google.com → 142.250.x.x
```

---

# DNS Record Types

## A Record

Maps a domain name to an IPv4 address.

Example:

```text
example.com → 192.168.1.10
```

---

## AAAA Record

Maps a domain name to an IPv6 address.

Example:

```text
example.com → 2001:db8::1
```

---

## CNAME Record

Creates an alias for another domain.

Example:

```text
www.example.com → example.com
```

---

## MX Record

Specifies mail servers responsible for receiving emails.

Example:

```text
gmail.com → mail servers
```

---

## NS Record

Specifies authoritative name servers for a domain.

Example:

```text
ns1.example.com
ns2.example.com
```

---

# dig Command Output

## Command

```bash
dig google.com
```

Sample Output:

```text
google.com. 300 IN A 142.250.183.14
```

### A Record

```text
142.250.183.14
```

### TTL

```text
300 seconds
```

### Observation

The DNS server successfully resolved the domain name into an IPv4 address.

---

# Task 2 – IP Addressing

# What is an IPv4 Address?

An IPv4 address is a unique numerical identifier assigned to a device on a network.

Example:

```text
192.168.1.10
```

Structure:

* Four octets
* Each octet ranges from 0–255
* Total size: 32 bits

Example Breakdown:

```text
192 . 168 . 1 . 10
```

Each section represents 8 bits.

---

# Public vs Private IP Addresses

## Public IP

A public IP address is reachable over the internet.

Example:

```text
3.121.220.5
```

Common Uses:

* Web servers
* APIs
* Public cloud services

---

## Private IP

A private IP address is used inside internal networks.

Example:

```text
10.0.1.15
```

Common Uses:

* EC2 to RDS communication
* Internal application traffic

Private IPs are not directly reachable from the internet.

---

# Private IP Ranges

RFC1918 defines three private ranges.

## Class A

```text
10.0.0.0 – 10.255.255.255
```

CIDR:

```text
10.0.0.0/8
```

---

## Class B

```text
172.16.0.0 – 172.31.255.255
```

CIDR:

```text
172.16.0.0/12
```

---

## Class C

```text
192.168.0.0 – 192.168.255.255
```

CIDR:

```text
192.168.0.0/16
```

---

# Checking Local IP Addresses

## Command

```bash
ip addr show
```

Sample Output:

```text
inet 172.31.2.182/20
```

Observation:

* This is a private IP address.
* Falls within the 172.16.x.x – 172.31.x.x range.

---

# Task 3 – CIDR & Subnetting

# What Does /24 Mean?

Example:

```text
192.168.1.0/24
```

The `/24` means:

* First 24 bits identify the network.
* Remaining 8 bits identify hosts.

Subnet Mask:

```text
255.255.255.0
```

---

# Why Do We Subnet?

Subnetting helps:

* Organize networks
* Improve security
* Reduce broadcast traffic
* Separate environments
* Efficiently allocate IP addresses

Example:

Separate networks for:

* Production
* Development
* Testing

---

# CIDR Reference Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Host Calculations

## /24

Hosts:

```text
2^(32-24) = 256
```

Usable:

```text
254
```

(Network + Broadcast reserved)

---

## /16

Hosts:

```text
65,536
```

Usable:

```text
65,534
```

---

## /28

Hosts:

```text
16
```

Usable:

```text
14
```

---

# Real AWS Example

A VPC may use:

```text
10.0.0.0/16
```

Subnets:

```text
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24
```

Benefits:

* Better organization
* Availability Zone separation
* Security isolation

---

# Task 4 – Ports: The Doors to Services

# What is a Port?

A port is a logical endpoint used by applications to receive network traffic.

An IP address identifies a machine.

A port identifies a specific service on that machine.

Example:

```text
192.168.1.10:22
```

* IP → Server
* Port → SSH Service

---

# Why Do We Need Ports?

A single server may run:

* SSH
* Nginx
* MySQL
* Redis

All simultaneously.

Ports allow these services to coexist on the same IP address.

---

# Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

# Common DevOps Ports

## SSH

```text
22
```

Remote server access.

---

## HTTP

```text
80
```

Web traffic.

---

## HTTPS

```text
443
```

Secure web traffic.

---

## DNS

```text
53
```

Name resolution.

---

## MySQL

```text
3306
```

Database access.

---

## Redis

```text
6379
```

Caching.

---

## MongoDB

```text
27017
```

NoSQL database.

---

# Checking Listening Ports

## Command

```bash
ss -tulpn
```

Sample Output

```text
tcp LISTEN 0 511 *:22
tcp LISTEN 0 511 *:80
```

### Interpretation

Port 22

```text
SSH Service
```

Port 80

```text
Nginx Web Server
```

---

# Task 5 – Putting It Together

# Scenario 1

## Command

```bash
curl http://myapp.com:8080
```

### Networking Concepts Involved

1. DNS resolves myapp.com into an IP address.
2. TCP establishes a connection.
3. Traffic is sent to port 8080.
4. HTTP protocol requests data from the application.

Concepts involved:

* DNS
* IP Addressing
* TCP
* Ports
* HTTP

---

# Scenario 2

Application cannot connect to:

```text
10.0.1.50:3306
```

### First Checks

1. Is the database service running?
2. Is port 3306 listening?
3. Is the destination IP reachable?
4. Are Security Groups allowing traffic?
5. Are firewall rules blocking access?
6. Is DNS resolving correctly (if hostname is used)?

---

# Real DevOps Example

A web application hosted on AWS cannot connect to MySQL.

Investigation:

```text
Application
      ↓
DNS
      ↓
Private IP
      ↓
Port 3306
      ↓
Security Group
      ↓
MySQL Server
```

Possible failures:

* Wrong DNS record
* Incorrect IP address
* Security Group block
* MySQL service stopped
* Firewall restriction

---

# What I Learned

## 1

DNS converts human-readable names into IP addresses.

---

## 2

CIDR notation determines network size and available hosts.

---

## 3

Ports allow multiple services to run on a single server.

---

# Key Takeaways

* DNS is the internet's phonebook.
* IP addresses uniquely identify devices.
* Private IPs are used internally.
* Public IPs are internet accessible.
* CIDR controls subnet size.
* Ports identify applications running on a server.
* Most cloud networking issues involve DNS, IPs, routes, firewalls, or ports.
* Understanding these concepts is essential for troubleshooting production systems.

---

# Conclusion

DNS, IP addressing, subnetting, and ports form the foundation of modern networking. Every cloud platform, container platform, and application depends on these concepts. As a DevOps engineer, mastering them improves troubleshooting skills, cloud architecture understanding, and overall system reliability.

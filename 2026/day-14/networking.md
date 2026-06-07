# Day 14 – Networking Fundamentals for DevOps Engineers

# Introduction

Networking is one of the most important skills in DevOps because every modern application depends on communication between multiple systems. A simple web application might involve a browser, DNS server, load balancer, web server, application server, database server, cache server, monitoring system, and cloud networking components. If communication fails between any of these layers, the application may become unavailable.

As DevOps engineers, we are often responsible for troubleshooting connectivity issues, configuring cloud networking, managing load balancers, securing communication between services, and ensuring applications remain available. Understanding networking fundamentals makes it easier to diagnose incidents and build reliable infrastructure.

---

# What is a Computer Network?

A computer network is a collection of devices connected together for communication and resource sharing.

Examples include:

* A laptop communicating with a website.
* An EC2 instance communicating with an RDS database.
* A Kubernetes Pod communicating with another Pod.
* A CI/CD server communicating with GitHub.
* A monitoring system collecting metrics from servers.

Networks allow devices to exchange information using standardized protocols.

Without networking:

* Websites cannot be accessed.
* Applications cannot communicate.
* Databases cannot receive requests.
* Cloud infrastructure cannot function.

---

# Why Networking Matters in DevOps

Networking is involved in almost every DevOps activity.

## Infrastructure Provisioning

When creating cloud infrastructure, engineers must configure:

* VPCs
* Subnets
* Route Tables
* Internet Gateways
* NAT Gateways
* Security Groups
* Network ACLs

These networking components determine how resources communicate.

---

## Application Deployment

Applications rarely exist on a single machine.

A typical deployment includes:

```text
User
 |
DNS
 |
Load Balancer
 |
Application Server
 |
Database
```

Each component communicates through the network.

---

## Containers

Containerized applications depend heavily on networking.

Examples:

* Frontend container communicates with backend container.
* Backend container communicates with database container.
* Containers communicate through Docker networks.

Without networking, microservices architecture would not work.

---

## Kubernetes

Networking is one of the most important Kubernetes concepts.

Requirements include:

* Pod-to-Pod communication
* Service discovery
* Cluster networking
* Ingress traffic
* External traffic routing

Many Kubernetes troubleshooting issues are networking-related.

---

# The OSI Model

The Open Systems Interconnection (OSI) model explains how data travels across a network.

It consists of seven layers.

---

# Layer 7 – Application Layer

This layer interacts directly with applications.

Protocols include:

* HTTP
* HTTPS
* DNS
* SSH
* FTP
* SMTP

Examples:

* Opening a website
* Connecting to a server using SSH
* Sending an email

DevOps relevance:

Most incidents are initially observed at this layer because users interact with applications.

---

# Layer 6 – Presentation Layer

Responsible for:

* Encryption
* Compression
* Data formatting

Examples:

* SSL/TLS encryption
* JSON formatting
* Image encoding

When HTTPS is used, encryption happens here.

---

# Layer 5 – Session Layer

Responsible for:

* Creating sessions
* Maintaining sessions
* Terminating sessions

Examples:

* User login sessions
* Persistent application connections

---

# Layer 4 – Transport Layer

Provides end-to-end communication.

Protocols:

* TCP
* UDP

Responsibilities:

* Reliability
* Error recovery
* Flow control
* Port management

Examples:

* HTTPS uses TCP
* DNS often uses UDP

---

# Layer 3 – Network Layer

Responsible for routing packets between networks.

Protocol:

* IP

Functions:

* Logical addressing
* Packet routing
* Path selection

Examples:

* Routing traffic between AWS regions
* Communication between subnets

---

# Layer 2 – Data Link Layer

Responsible for communication within the same network segment.

Functions:

* MAC addressing
* Switching
* Frame transmission

Devices:

* Switches

---

# Layer 1 – Physical Layer

The lowest layer.

Includes:

* Fiber cables
* Ethernet cables
* Wireless signals
* Network hardware

Cloud providers abstract most physical infrastructure from users.

---

# TCP/IP Model

Although the OSI model is useful for learning, the TCP/IP model is used in practice.

It consists of four layers:

## Application Layer

Protocols:

* HTTP
* HTTPS
* DNS
* SSH

---

## Transport Layer

Protocols:

* TCP
* UDP

---

## Internet Layer

Protocols:

* IP
* ICMP

---

## Network Access Layer

Examples:

* Ethernet
* Wi-Fi

---

# Understanding IP Addresses

Every device connected to a network requires an IP address.

An IP address identifies a device uniquely within a network.

---

# IPv4

Example:

```text
192.168.1.10
```

Characteristics:

* 32-bit address
* Approximately 4.3 billion addresses

---

# IPv6

Example:

```text
2001:db8::1
```

Characteristics:

* 128-bit address
* Extremely large address space

IPv6 was created because IPv4 addresses are limited.

---

# Public and Private IP Addresses

## Public IP

Reachable from the internet.

Example:

```text
3.121.220.5
```

Used by:

* Public websites
* Public APIs

---

## Private IP

Used inside private networks.

Ranges:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

Examples:

* EC2 communicating with RDS
* Internal application communication

---

# Understanding Ports

A single server can host multiple services simultaneously.

Ports identify which application should receive traffic.

Examples:

| Port  | Service    |
| ----- | ---------- |
| 22    | SSH        |
| 80    | HTTP       |
| 443   | HTTPS      |
| 3306  | MySQL      |
| 5432  | PostgreSQL |
| 6379  | Redis      |
| 27017 | MongoDB    |

When a browser accesses:

```text
https://example.com
```

It connects to:

```text
example.com:443
```

---

# TCP vs UDP

## TCP

Features:

* Connection-oriented
* Reliable
* Ordered delivery
* Error checking

Examples:

* HTTPS
* SSH
* Databases

Advantages:

* Reliable communication

Disadvantages:

* Slightly slower

---

## UDP

Features:

* Connectionless
* Faster
* No delivery guarantee

Examples:

* DNS
* Video streaming
* Online gaming

Advantages:

* High performance

Disadvantages:

* Possible packet loss

---

# DNS (Domain Name System)

DNS translates domain names into IP addresses.

Example:

```text
google.com
```

becomes:

```text
142.250.x.x
```

Without DNS, users would need to remember IP addresses.

---

# DNS Resolution Process

When a user visits:

```text
https://google.com
```

The following happens:

1. Browser checks local cache.
2. Operating system checks DNS cache.
3. Resolver queries DNS server.
4. DNS server returns IP address.
5. Browser connects to destination.

---

# Load Balancers

Load balancers distribute traffic across multiple servers.

Benefits:

* Scalability
* High availability
* Fault tolerance

Architecture:

```text
Users
 |
Load Balancer
 |
-------------------
|        |        |
App1    App2    App3
```

Common Types:

* AWS Application Load Balancer
* AWS Network Load Balancer
* Nginx
* HAProxy

---

# Firewalls and Security Groups

Firewalls control incoming and outgoing traffic.

AWS uses:

* Security Groups
* Network ACLs

Example:

Allow:

```text
22
80
443
```

Block:

```text
All other ports
```

Principle:

Grant only required access.

---

# Networking in Docker

Docker creates isolated virtual networks.

Common network types:

## Bridge Network

Default Docker network.

Used for:

* Container-to-container communication

---

## Host Network

Container shares host network stack.

---

## Overlay Network

Used across multiple Docker hosts.

Important in Docker Swarm.

---

# Networking in Kubernetes

Every Pod receives an IP address.

Requirements:

* Every Pod can communicate with every other Pod.
* Services provide stable endpoints.
* Ingress manages external traffic.

Components:

* Pod
* Service
* Ingress
* CoreDNS

---

# Common Networking Problems

## DNS Failure

Symptoms:

* Website inaccessible
* API calls fail

Root Causes:

* Wrong DNS records
* Resolver issues

---

## Firewall Blocking Traffic

Symptoms:

* Service unreachable

Root Causes:

* Closed port
* Incorrect Security Group

---

## Load Balancer Misconfiguration

Symptoms:

* Intermittent failures

Root Causes:

* Incorrect target group
* Health check failures

---

## SSL Certificate Issues

Symptoms:

* HTTPS warnings

Root Causes:

* Expired certificate
* Invalid certificate chain

---

# DevOps Troubleshooting Workflow

When an application is down:

## Step 1

Check DNS.

## Step 2

Check network connectivity.

## Step 3

Check route to destination.

## Step 4

Check listening ports.

## Step 5

Check firewall rules.

## Step 6

Check application logs.

## Step 7

Check system resources.

## Step 8

Check cloud networking configuration.

---

# Real Production Example

A website becomes inaccessible.

Investigation flow:

1. Verify DNS resolution.
2. Verify Load Balancer health.
3. Verify Security Group rules.
4. Verify Nginx service.
5. Verify application process.
6. Verify database connectivity.
7. Review logs.
8. Check CPU, memory, and disk utilization.

This systematic approach prevents guesswork and reduces downtime.

---

# Key Takeaways

* Networking is the backbone of modern infrastructure.
* DNS, TCP/IP, and HTTP are used daily by DevOps engineers.
* Cloud infrastructure relies heavily on networking concepts.
* Understanding ports, protocols, and routing speeds up troubleshooting.
* Containers and Kubernetes depend on networking for communication.
* Most production incidents involve networking somewhere in the request path.

---

# Conclusion

Networking is one of the foundational pillars of DevOps. Whether deploying applications on AWS, managing Docker containers, operating Kubernetes clusters, configuring load balancers, or troubleshooting production incidents, networking knowledge is essential. Strong networking fundamentals help engineers identify problems faster, communicate effectively with teams, and build highly available, scalable systems.

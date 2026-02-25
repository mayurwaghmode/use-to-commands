# 🐧 Linux Commands – DevOps / SRE Quick Reference

A practical and concise reference guide for commonly used Linux commands with real-world DevOps and SRE use cases.

---

# 📌 1️⃣ lsof – List Open Files

## 🔹 Overview

`lsof` stands for **List Open Files**.

In Linux, everything is treated as a file:
- Regular files
- Directories
- Network sockets
- Devices
- Pipes

`lsof` helps identify which process is using which file or network resource.

---

## 🔹 Syntax

```bash
lsof [options]
```

## 🔹 Common Use Cases
### ✅ 1. Find which process is using a specific port

```bash
lsof -i :8080
```

Use Case:

Debug “Port already in use” errors

Identify service bound to a specific port

### ✅ 2. List files opened by a specific process (PID)
```bash
lsof -p <PID>
```

Use Case:

Debug memory/file descriptor leaks

Analyze application resource usage

### ✅ 3. Identify which process is using a file
```bash
lsof /var/log/app.log
```
Use Case:

Unable to delete a file

Log rotation troubleshooting

File lock investigation

### ✅ 4. List all network connections
```bash
lsof -i
```
🎯 Interview Explanation

lsof is used to identify open files and network sockets by processes. It helps troubleshoot port conflicts, file locks, and resource exhaustion issues.

##📌 2️⃣ netstat – Network Statistics
🔹 Overview

netstat is used to monitor:

Active network connections

Listening ports

Routing tables

Interface statistics

Protocol statistics

⚠️ Note: netstat is deprecated in many modern Linux distributions. Use ss instead.

🔹 Syntax
```bash
netstat [options]
```
🔹 Common Use Cases
### ✅ 1. Check listening ports
```bash
netstat -tuln

Options:

-t → TCP

-u → UDP

-l → Listening

-n → Numeric output (no DNS resolution)
```

Use Case:

Verify service is running

Confirm application binding to correct port

### ✅ 2. Identify process using a port
```bash
netstat -tulnp

(-p shows PID and program name)
```

Use Case:

Find which service is occupying a port

### ✅ 3. View active connections
```bash
netstat -an

Use Case:

Check ESTABLISHED connections

Investigate suspicious traffic

Analyze connection states (TIME_WAIT, CLOSE_WAIT)
```

### ✅ 4. Show routing table
```bash
netstat -r

Use Case:

Troubleshoot network routing issues

📌 Modern Alternative – ss
ss -tulnp
Why prefer ss?
```
Faster

More detailed output

Better performance on production systems

Replaces netstat in modern Linux distributions

🚀 Production Troubleshooting Scenarios
Scenario	Command
Port already in use	lsof -i :PORT
Application not reachable	netstat -tuln
High number of connections	netstat -an
Cannot delete file	lsof filename
Verify service binding	ss -tulnp

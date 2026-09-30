# ⚡ PHP Command Execution & OS Command Injection

<p align="center">
  <img src="https://img.shields.io/badge/PHP-Command%20Execution-777BB4?style=for-the-badge&logo=php&logoColor=white">
  <img src="https://img.shields.io/badge/Cybersecurity-Learning-111827?style=for-the-badge&logo=hackthebox&logoColor=white">
  <img src="https://img.shields.io/badge/Web%20Security-Lab-DC2626?style=for-the-badge&logo=owasp&logoColor=white">
  <img src="https://img.shields.io/badge/Status-Educational-16A34A?style=for-the-badge">
</p>

<p align="center">
  <b>Understanding PHP OS Command Execution & Web Application Security</b>
</p>

---

## 🧠 About This Lab

This repository documents my learning journey with **PHP command execution functions** and the security risks associated with allowing untrusted input to interact with operating-system commands.

The goal is to understand:

* How PHP interacts with the operating system
* Differences between PHP command-execution functions
* How insecure input handling can create security vulnerabilities
* The fundamentals of **OS Command Injection**
* Secure coding and defensive practices

> 🔐 **This repository is for educational and authorized security testing only.**

---

## 🚀 Topics Covered

```text
PHP Command Execution
        │
        ├── system()
        ├── passthru()
        ├── shell_exec()
        ├── exec()
        ├── PHP Backticks
        │
        └── Security Implications
                │
                ├── Command Injection
                ├── Input Validation
                ├── Secure Coding
                └── Least Privilege
```

---

# 🔧 PHP Command Execution Functions

## First Cheak
```php
#For Information:
<?phpinfo();?>
```

## 01 — `system()`

`system()` executes an operating-system command and normally sends its output directly to the output stream.

```php
# Execute one command
<?php system("whoami"); ?>
```
#### Extra:
```php
# Take input from the url paramter. shell.php?cmd=whoami
 system($_GET['cmd']);
```
```text
PHP
 ↓
system()
 ↓
Operating System
 ↓
Command
 ↓
Output
```

---

## 02 — `passthru()`

`passthru()` executes an external command and passes the output directly to the output stream.

```php
# The same but using passthru
<?php passthru($_GET['cmd']); ?>
```

### Key Point

Useful when the command output needs to be passed through directly.

---

## 03 — `shell_exec()`

`shell_exec()` executes a command and returns its output as a string.

```php
# For shell_exec to output the result you need to echo it
<?php echo shell_exec("whoami");?>

```

## 04 — `exec()`

`exec()` executes an external command.

It can return the last line of output and can also populate an array with output lines.

```php
# Exec() does not output the result without echo, and only output the last line. So not very useful!
<?php echo exec("whoami");?>
```
#### Extra:

```php
# Instead to this if you can. It will return the output as an array, and then print it all.
<?php exec("ls -la",$array); print_r($array); ?>

 ```
## 05 — PHP Backticks

PHP also provides another syntax for executing shell commands:

```php
# Using backticks
<?php $output = `whoami`; echo "<pre>$output</pre>"; ?>
```
#### Extra:
```php
# Using backticks
<?php echo `whoami`; ?>

```
This is conceptually similar to obtaining command output through `shell_exec()`.

---
## 06 `preg_replace()`
```php
# preg_replace(). This is a cool trick
<?php preg_replace('/.*/e', 'system("whoami");', ''); ?>
```
---

# 📊 Function Comparison

| Function       | OS Command | Output                 |
| :------------- | :--------: | :--------------------- |
| `system()`     |      ✅     | Direct output          |
| `passthru()`   |      ✅     | Direct output          |
| `shell_exec()` |      ✅     | Returns string         |
| `exec()`       |      ✅     | Returns output / array |
| Backticks      |      ✅     | Returns command output |

---

# 🚨 Security Perspective

The most important security concept in this lab is **untrusted input**.

A dangerous application pattern looks conceptually like:

```text
┌──────────────────┐
│   User Input     │
└────────┬─────────┘
         ↓
┌──────────────────┐
│   PHP Application│
└────────┬─────────┘
         ↓
┌──────────────────┐
│ OS Command Layer │
└────────┬─────────┘
         ↓
┌──────────────────┐
│ Operating System │
└──────────────────┘
```

If an application allows arbitrary user input to reach an OS command, an attacker may potentially influence what the server executes.

This class of vulnerability is commonly known as:

> **OS Command Injection**

---

# 🛡️ Secure Coding

When building real-world applications:

### ❌ Avoid

```text
User Input
    ↓
OS Command
```

### ✅ Prefer

```text
User Input
    ↓
Strict Validation
    ↓
Allowlisted Values
    ↓
Safe Application Logic
```

### Security Practices

* 🔒 Never trust user input.
* ✅ Validate input strictly.
* ✅ Prefer native PHP functionality where possible.
* ✅ Use allowlists for expected values.
* ❌ Avoid unnecessary OS command execution.
* 🔐 Follow least-privilege principles.
* 🔄 Keep PHP and server software updated.
* 🧪 Perform security testing in isolated labs.

---

# 🧪 Recommended Lab Setup

For learning and experimentation, use an isolated environment:

```text
             ┌─────────────────────┐
             │   Local PHP Lab     │
             └──────────┬──────────┘
                        │
                        ▼
             ┌─────────────────────┐
             │ Vulnerable Practice │
             │     Application     │
             └──────────┬──────────┘
                        │
                        ▼
             ┌─────────────────────┐
             │   Isolated VM/Lab   │
             └─────────────────────┘
```

Only test systems that you **own or have explicit authorization to assess**.

---

# 🎯 Learning Objectives

By completing this lab, I aim to understand:

* [x] PHP OS command execution
* [x] `system()`
* [x] `passthru()`
* [x] `shell_exec()`
* [x] `exec()`
* [x] PHP backticks
* [x] Basic command injection concepts
* [x] Input validation
* [x] Secure coding principles
* [x] Least-privilege concepts

---

# 🌐 Web Security Connection

This topic connects with several important areas of application security:

```text
                 WEB SECURITY
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
   Input          Command         Server
 Validation       Injection       Security
       │              │              │
       └──────────────┼──────────────┘
                      ▼
               Secure Development
```

Understanding command execution is useful when studying:

* Web Application Security
* VAPT
* Secure Coding
* Server-Side Security
* OWASP concepts
* Vulnerability Assessment
* Application Security

---


# 📚 Learning Notes

### Command Execution

PHP provides multiple mechanisms for interacting with external commands.

### Command Injection

Command Injection occurs when an application improperly allows attacker-controlled input to influence commands executed by the operating system.

### Root Cause

The fundamental problem is usually:

```text
Untrusted Input
      +
Unsafe Command Construction
      =
Potential Command Injection
```

---

# ⚠️ Responsible Use

This repository is intended strictly for:

* 🎓 Learning
* 🧪 Authorized labs
* 🔐 Defensive security research
* 💻 Local testing
* 📚 Cybersecurity education

**Do not use these techniques against systems without explicit authorization.**

---

# 👨‍💻 Author

<p align="center">

### Abdullah Al Faruk

**Software Engineering Student • Cybersecurity Enthusiast**

Web Application Security • VAPT • Python • Linux • Web Security

</p>

---

## ⭐ Support

If this repository helped you understand PHP command execution and web application security concepts, consider giving it a ⭐.

---

<p align="center">
  <b>⚡ Learn • Build • Secure ⚡</b>
</p>

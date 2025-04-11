# LEKIR - Remote Code Execution (RCE) 

![Security Banner](https://img.shields.io/badge/Security-Research-blue) 
![Educational](https://img.shields.io/badge/Purpose-Educational-green)

- Write-Up Author: whoami \[[whoami]([firdauskhairuddin](https://github.com/firdauskhairuddin))\]
- Flag: firdausmemanghensem

A repository documenting my learning journey about Remote Code Execution vulnerabilities, particularly in PHP environments.

## 📌 Overview

Remote Code Execution (RCE) is a critical security vulnerability that allows attackers to execute arbitrary commands on a target server. This repository contains my notes, payloads, and mitigation strategies learned while studying RCE vulnerabilities.

## 🔥 Key Concepts

### What is RCE?
- Allows attackers to execute commands on a remote system
- Often achieved through injection vulnerabilities
- Can lead to complete system compromise
- Commonly rated as Critical severity (CVSS 9.0+)

### Common Attack Vectors:
- Unsanitized user input passed to execution functions
- Insecure file upload handling
- Dangerous deserialization
- Server-side template injection

## 💻 Dangerous PHP Functions

These PHP functions can lead to RCE if used improperly with user input:

| Function       | Risk Level | Description |
|----------------|------------|-------------|
| `exec()`       | High       | Executes external program |
| `system()`     | High       | Executes command and displays output |
| `passthru()`   | High       | Executes command and displays raw output |
| `shell_exec()` | High       | Executes command via shell |
| Backticks (`` ` ``) | High | Same as shell_exec() |
| `popen()`      | Medium     | Opens process file pointer |
| `proc_open()`  | Medium     | Advanced process control |

## 🛠️ Example Procedure
![Screenshot 2025-04-11 125153](https://github.com/user-attachments/assets/025d756b-5b10-4325-94e7-2fbb603b1cda)

## Challenge Description:

>this is challenge description
Level : Others
Short Form : RCE
Injection Point : $_POST['calculate']
Why this happen : It's a vulnerability that allows an attacker to execute arbitrary code on a target system remotely. Attackers exploit this vulnerability by injecting malicious code into an application or system, often through input fields or file uploads. Once exploited, RCE can lead to complete compromise of the target system, allowing attackers to steal data, install malware, or take control of the system. To prevent RCE vulnerabilities, applications should sanitize user input, validate file uploads, and implement proper security controls to restrict code execution.































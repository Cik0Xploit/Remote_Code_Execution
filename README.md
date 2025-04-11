# LEKIR - Remote Code Execution (RCE) Learning Repository

![Security Banner](https://img.shields.io/badge/Security-Research-blue) 
![Educational](https://img.shields.io/badge/Purpose-Educational-green)

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


## Procedure

## 🛠️ Example 
![Screenshot 2025-04-11 125153](https://github.com/user-attachments/assets/025d756b-5b10-4325-94e7-2fbb603b1cda)

![image](https://github.com/user-attachments/assets/c24c9aca-868b-4f42-aa3b-008f8cb2599e)

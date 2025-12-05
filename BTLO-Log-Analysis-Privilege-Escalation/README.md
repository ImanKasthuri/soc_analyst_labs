# BTLO Log Analysis Privilege Escalation

## Overview

This lab demonstrates an investigation of the attacker's bash history. There were no signs of hacking because no one logged in to the server; instead, the attacker used a hidden weakness in the website. The attacker used the ```x.phtml``` malicious file to get remote access to the website and find the server's vulnerabilities. With the use of X.phtml malicious file, attacker discovered that Python enabled the SUID, which will help them to gain root access in the server. The attacker deleted x.phtml to hide the evidence that would make them harder to detect.

## Tools Used
NotePad ++

## What user (other than ‘root’) is present on the server?

I discovered that the attacker accessed Daniel's home directory.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6b597852-93bd-48c0-a8cf-6da61c14b050" />

## What script did the attacker try to download to the server?

The attacker downloaded the ```linux-exploit-suggester.sh```. Which is well known script attacker used to:
- Scan the server
- Find kernal vulnerabilities
- Help them become root

Attacker downloaded the file as ```les.sh```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cc1efe7d-6bba-49f9-a7fb-65b3cd88c0ed" />

## What packet analyzer tool did the attacker try to use? 

The attacker used tcpdump to spy on network server's traffic so they could steal data, find new target and avoid getting caught.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b5386466-cdfe-4ddf-9ed2-81e8d6a138a1" />

## What file extension did the attacker use to bypass the file upload filter implemented by the developer?

Attacker used ```x.phtml``` malicious file to remote access through the website.

They used this website to:
- Run commands
- explore directories
- To gain high previlage
- Eventually become the root

After they were done with the work they deleted it because:
- Makes the attack harder to detect
- Hides evidence
- Make it looks nothing happened

```rm /var/www/html/uploads/x.phtml```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5f29a38b-86e1-42c7-ba05-6a2252e2ad09" />

## Based on the commands run by the attacker before removing the php shell, what misconfiguration was exploited in the ‘python’ binary to gain root-level access? 1- Reverse Shell ; 2- File Upload ; 3- File Write ; 4- SUID ; 5- Library load 

```/usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'``` In this case, enabled SUID, it is a huge vulnerability for the server. So the Python runs as root, which means the attacker can also get root privilege using Python.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/61aab1f9-6c2c-4ada-85a4-924209a01d81" />










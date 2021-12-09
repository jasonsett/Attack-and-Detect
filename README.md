# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
#### Nmap scan results for each machine reveal the below services and OS details:

Target 1
```bash
$ nmap -sV --version-all 192.168.1.110
```
![](Images/sVscan_Target1.png)

Target 2
```bash
$ nmap -sV -O 192.168.1.115
```
![](Images/sVscan_Target2.png)

ELK Server
```bash
$ nmap -sV --version-all 192.168.1.100
```
![](Images/sVscan_ELK.png)

Capstone
```bash
$ nmap -sV --version-all 192.168.1.105
```
 ![](Images/sVscan_Capstone.png)

Kali
```bash
$ nmap -sV --version-all 192.168.1.90
```
![](Images/sVscan_Kali.png)

NAT Switch
```bash
$ nmap -sV --version-all 192.168.1.1
```
![](Images/sVscan_NAT.png)

#### This scan identifies the services below as potential points of entry for Targets 1 and 2:
- Target 1
| PORT     | STATE      | SERVICE    | VERSION                                      |
|----------|------------|------------|----------------------------------------------|
| 22/tcp   | open       | ssh        | OpenSSH 6.7p1 Debian 5+deb8u4 (protocol 2.0) |
| 80/tcp   | open       | http       | Apache httpd 2.4.10 (Debian)                 |

- Target 2
| PORT     | STATE      | SERVICE    | VERSION                                      |
|----------|------------|------------|----------------------------------------------|
| 22/tcp   | open       | ssh        | OpenSSH 6.7p1 Debian 5+deb8u4 (protocol 2.0) |
| 80/tcp   | open       | http       | Apache httpd 2.4.10 (Debian)                 |

#### The following vulnerabilities were identified on Target 1:

- Exposure of Information through Directory Listing (CWE-548)\
- Severity: Low\
![](Images/WP_directory.png)
![](Images/michael_directory.png)
![](Images/WP_xmlrpc.php)
![](Images/(wp-login.php)
![](Images/WP_OS_version.png)

- Weak Password Requirements (CWE-521)
- Severity: High
![](Images/michael_ssh.png)
![](Images/(cracking_steven.png)

- Improper Access Control (CWE-284)
- Severity: High
![](Images/wp-config.php.png)
![](Images/WPDB_login.png)
![](Images/hashed_pwds.png)

- Improper Privilege Management (CWE-269)
- Severity: High
![](Images/root_escalation.png)

#### In addition to the vulnerabilites above, these vulnerabilities were exploited on Target 2:
- Critical Vulnerability 1 (CWE/CVE#)
- Severity:
	_TODO: INSERT SCREENSHOTS HERE_

- Critical Vulnerability 2 (CWE/CVE#)
- Severity:
	_TODO: INSERT SCREENSHOTS HERE_

- Critical Vulnerability 3 (CWE/CVE#)
- Severity:
	_TODO: INSERT SCREENSHOTS HERE_

### Exploitation
#### The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- `flag1.txt`: _b9bbcb33e11b80be759c4e844862482d_
  - **Exploit Used: _CWE-548: Exposure of Information through Directory Listing_**
  - _Command: $ nano /var/www/html/service.html_
![](Images/t1_flag1.png)

- `flag2.txt`: _fc3fd58dcdad9ab23faca6e9a36e581c_
  - **Exploit Used: _CWE-521: Weak Password Requirements_**
  - _Command: $ cat /var/www/flag2.txt_
![](Images/t1_flag2.png)

- `flag3.txt`: _afc01ab56b50591e7dccf93122770cd2_
  - **Exploit Used: _CWE-284: Improper Access Control_**
  - _Command: $ mysql> SELECT * FROM wp_posts;_
![](Images/t1_flag3-4.png)

- `flag4.txt`: _715dea6c055b9fe3337544932f2941ce_
  - **Exploit Used: _CWE-269: Improper Privilege Management**
  - _Command: $ sudo python -c 'import pty;pty.spawn("bin/bash")'_
![](Images/root_escalation.png)
![](Images/t1_flag4.png)

#### The team also penetrated `Target 2` and retrieved additional confidential data:
- `flag1.txt`: _a2c1f66d2b8051bd3a5874b5b6e43e21_
  - **Exploit Used: _TODO: Identify the exploit used_**
  - _URL: 192.168.1.115/vendor/PATH_
![](Images/t2_flag1.png)

- `flag2.txt`: _6a8ed560f0b5358ecf844108048eb337_
  - **Exploit Used: _TODO: Identify the exploit used_**
  - _Command: $ cat /var/www/flag2.txt_
![](Images/t2_flag2.png)

- `flag3.txt`: _a0f568aa9de277887f37730d71520d9b_
  - **Exploit Used: _TODO: Identify the exploit used_**
  - _URL: 192.168.1.115/wordpress/wp-content/uploads/2018/11/flag3.png_
![](Images/t2_flag3.png)
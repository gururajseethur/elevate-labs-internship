# Task 3

# Basic Vulnerability Scan (Cyber Security Internship)

## Objective

Perform a vulnerability scan on my local machine using OpenVAS (Greenbone Vulnerability Manager) and supporting tools.    
Identify vulnerabilities, assess severity (CVSS), and document remediation steps.

## Tools Used

 Kali Linux (2025.1)  
 OpenVAS (GVM) – Community Edition  
 Nmap 7.94  
 Lynis 3.0.9

## Steps Performed

1\. Installed GVM on Kali:    
   \`\`\`bash  
   sudo apt update && sudo apt install gvm y  
   sudo gvmsetup  
   sudo gvmstart

2. Logged in at `https://127.0.0.1:9392/` with admin account.

3. Created new **Target** → `127.0.0.1`.

4. Created **Task** → Full & Fast scan.

5. Ran scan → exported report in PDF.

6. Took screenshots of dashboard, vulnerabilities, and CVE details.

7. Ran quick local tools:

   * `nmap sS sV 127.0.0.1 oN report/nmapoutput.txt`

   * `lynis audit system > report/lynis.txt`

---

## **Key Findings (Sample / Mock)**

Replace with actual results once your scan finishes.

* **Critical:** OpenSSL 1.1.1k outdated → CVE20213449 (CVSS 9.8)

* **High:** SMBv1 protocol enabled (CVSS 7.5)

* **Medium:** Missing Linux kernel patches (CVSS 6.5)

* **Low:** Telnet port open (port 23, CVSS 4.0)

---

## **Conclusion**

* Successfully ran a vulnerability scan using GVM.

* Learned to interpret CVSS scores and prioritize remediation.

* Complemented scan with **Nmap** and **Lynis** for validation.

---

**Notes**

 Vulnerability 1  
 Title: Outdated OpenSSL  
 CVE: CVE20213449  
 CVSS: 9.8 (Critical)  
 Impact: Remote code execution via TLS handshake.  
 Remediation: Update OpenSSL with \`sudo apt update && sudo apt upgrade openssl y\`.

 Vulnerability 2  
 Title: SMBv1 Protocol Enabled  
 CVSS: 7.5 (High)  
 Impact: SMBv1 is deprecated and vulnerable to EternalBluetype exploits.  
 Remediation: Disable SMBv1, enable SMBv2/3, or block port 445 if unused.

 Vulnerability 3  
 Title: Missing Linux Kernel Patches  
 CVSS: 6.5 (Medium)  
 Impact: Kernel privilege escalation possible.  
 Remediation: Apply latest kernel updates with \`aptget distupgrade\`.

 Vulnerability 4  
 Title: Telnet Service Detected  
 CVSS: 4.0 (Low)  
 Impact: Unencrypted credentials if used.  
 Remediation: Disable Telnet, use SSH instead.

---


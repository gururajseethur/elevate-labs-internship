# Elevate Labs Cybersecurity Internship

<p>
<img src="https://img.shields.io/badge/internship-Elevate%20Labs-purple" alt="elevate labs" />
<img src="https://img.shields.io/badge/focus-Cybersecurity-blue" alt="focus" />
<img src="https://img.shields.io/badge/status-Complete-success" alt="status" />
</p>

Deliverables from my cybersecurity internship with **Elevate Labs** — three guided tasks,
each with a written report and whatever evidence the task produced.

## Tasks

| # | Task | What it covers | Evidence |
|---|------|----------------|----------|
| 1 | [Local network port scan](CyberSec-Task1) | Discovery and service enumeration across a `/24`, SMB enumeration via NSE, then a re-scan after patching | Raw `nmap` output, packet capture, interview Q&A |
| 2 | [Phishing email analysis](Cybersec%20Task%202) | Header inspection, sender and link analysis, social-engineering indicators, and a summary of the phishing traits found | Written report with annotated screenshots |
| 3 | [Vulnerability scan](Cybersec%20Task%203) | OpenVAS/GVM scan of a local host, CVSS severity assessment, and documented remediation steps | Written report |

## Environment and tools

All work ran on **Kali Linux** against a self-owned lab network (`192.168.80.0/24`).

`nmap 7.94` · `OpenVAS (GVM)` · `Lynis 3.0.9` · `Wireshark`

## What I took from it

Structured discovery does most of the work. The port scan only became useful once I
re-scanned after patching and could show the delta — a finding without a before-and-after
is just a screenshot.

The phishing task was the odd one out and the most useful. Reading headers by hand taught
me more about how mail actually moves than any tool would have, and it is the task closest
to what an analyst does on a real shift.

---

Part of my broader cybersecurity learning track — CEH, the BIA Master-Diploma in Cyber Security & Ethical Hacking, and [TryHackMe](https://tryhackme.com/p/Gururajseethur).

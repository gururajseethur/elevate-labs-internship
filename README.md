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
| 1 | [Local network port scan](task-1-network-port-scan) | Discovery across a `/24`, service and OS detection on the one responding host, an SMB NSE scan, and a verification re-scan | Raw `nmap` output from all three scans, plus interview Q&A |
| 2 | [Phishing email analysis](task-2-phishing-email-analysis/report.md) | Header inspection, sender and link analysis, social-engineering indicators, and a summary of the phishing traits found | Written report with one embedded screenshot |
| 3 | [Vulnerability scan](task-3-vulnerability-scan) | OpenVAS/GVM scan of a local host, then CVSS triage worked through on four representative findings | Written report |

## Environment and tools

All work ran on **Kali Linux** against a self-owned lab network (`192.168.80.0/24`).

`nmap 7.95` · `OpenVAS (GVM)` · `lynis 3.0.9`

## Honesty notes

Worth stating plainly, because the raw output is in the repository and contradicts the
tidier version of this story:

- The task 1 re-scan ran two minutes after the service scan and returned **the same five
  ports**. No remediation had been applied in between, so there is no before-and-after
  delta — the re-scan confirms the exposure persisted.
- The SMB NSE scripts returned **no script output**. The scan shows 139 and 445 open; it
  does not show the shares enumerated.
- The task 3 GVM report was exported as a PDF and is not published here. The findings
  table in that report is a worked CVSS triage exercise on representative vulnerability
  classes, labelled as such — it is not scan output.

## What I took from it

The port scan taught me more by failing than it would have by working. The NSE scripts
came back empty and the re-scan came back identical, and writing that down honestly is
harder — and more like the job — than presenting a clean delta would have been. A scan is
evidence of what responded, not of what you hoped to find.

The phishing task was the most useful of the three. Reading headers by hand taught me more
about how mail actually moves than any tool would have, and it is the task closest to what
an analyst does on a real shift.

---

Part of my broader cybersecurity learning track — CEH, the BIA Master-Diploma in Cyber Security & Ethical Hacking, and [TryHackMe](https://tryhackme.com/p/Gururajseethur).

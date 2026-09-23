# Task 1 — Local Network Port Scan

Discovery and service enumeration across a self-owned `/24`, followed by a verification
re-scan. Run 22 September 2025 from a Kali Linux VM (`192.168.80.128`, `eth0`) against
`192.168.80.0/24`, using `nmap 7.95`.

## What was run

| Step | Command | Output |
|---|---|---|
| Discovery | `sudo nmap -sS 192.168.80.0/24` | Not retained — the summary below is what it produced |
| Service and OS detection | `sudo nmap -sV -O -p 135,139,445,2869,7070 192.168.80.1` | [`nmap_deep_192.168.80.1.txt`](nmap_deep_192.168.80.1.txt) |
| SMB enumeration | `sudo nmap --script smb-enum-shares,smb-os-discovery,smb-security-mode -p 139,445 192.168.80.1` | [`nmap_smb_enum_192.168.80.1.txt`](nmap_smb_enum_192.168.80.1.txt) |
| Verification re-scan | `sudo nmap -sS -p 135,139,445,2869,7070 192.168.80.1` | [`post_patch_192.168.80.1.txt`](post_patch_192.168.80.1.txt) |

## Findings

Three hosts responded on the subnet:

- **`192.168.80.1`** — 135/msrpc, 139/netbios-ssn, 445/microsoft-ds, 2869/http (Microsoft
  HTTPAPI 2.0, SSDP/UPnP) and 7070/ssl. MAC `00:50:56:C0:00:08`, one hop away. The OUI is
  VMware's and the OS fingerprint came back Windows with no exact match, so this is the
  Windows host machine reached through its VMware virtual adapter rather than a separate
  device — its own SMB, RPC and UPnP services exposed to the lab network.
- **`192.168.80.254`** — filtered, no responding ports.
- **`192.168.80.128`** — the Kali VM itself, all scanned ports closed.

The SMB NSE scripts confirmed 139 and 445 open but **returned no script output** — no share
list, no OS discovery, no security-mode result. Either the host refused the null session or
the scripts were blocked; the scan is evidence that the ports are open, not that the shares
were enumerated.

The verification re-scan ran two minutes after the service scan and returned **the same five
ports in the same state**. Nothing had changed between the two scans — the re-scan confirms
the exposure persisted, it does not show remediation taking effect.

## Risk assessment

| Port | Service | Risk |
|---|---|---|
| 135 | MSRPC | Endpoint mapper; useful to an attacker for reconnaissance and lateral movement |
| 139, 445 | NetBIOS, SMB | File-share exposure and the usual target for lateral movement; high risk if SMBv1 is still enabled or the host is unpatched |
| 2869 | UPnP / SSDP | Can allow unauthenticated port mapping and leaks device information |
| 7070 | ssl/realserver | Vendor service; exposure depends entirely on the version behind it, which `-sV` could not fingerprint |

## Remediation recommended

1. Patch the host at `192.168.80.1`.
2. Disable SMBv1 and restrict SMB to trusted hosts.
3. Disable UPnP on the gateway if it is not needed.
4. Block 135, 139 and 445 at the host firewall for anything off-subnet.
5. Close 7070 if the service behind it is not in use.

None of these had been applied at the time of the re-scan.

## Files

- [`nmap_deep_192.168.80.1.txt`](nmap_deep_192.168.80.1.txt) — service and OS detection
- [`nmap_smb_enum_192.168.80.1.txt`](nmap_smb_enum_192.168.80.1.txt) — SMB NSE scan
- [`post_patch_192.168.80.1.txt`](post_patch_192.168.80.1.txt) — verification re-scan
- [`interview-questions.txt`](interview-questions.txt) — task Q&A

## Scope

All scanning was performed against my own VMs and my own local network.

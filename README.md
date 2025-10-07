# Basic Vulnerability Scan Report — Localhost

**Analyst:** Aman Rajak  
**Date:** 2025-09-25  
**Tool:** Nessus Essentials (local scan)  
**Scan source file:** `sample_report_127.0.0.1.txt` (raw scan output)

## Summary
A Nessus Essentials scan of the local host (`localhost` / `example`) was performed. The scan output shows a running Nessus web interface (port 8834) and a set of installed server packages and libraries (Apache, nginx, OpenSSL, PHP, PostgreSQL, OpenJDK, libcurl, etc.). The findings include services and package versions that should be reviewed and patched where required. Evidence and raw output are included in this repository.

_Source of findings: raw scan output file `sample_report_127.0.0.1.txt`._ :contentReference[oaicite:0]{index=0}

## Host metadata (observed)
- Hostname / RDNS: **localhost** / `example`. :contentReference[oaicite:1]{index=1}  
- OS / Kernel: **Linux (Kali)** — kernel `6.12.13-amd64`. :contentReference[oaicite:2]{index=2}  
- Nessus web UI listening on port **8834** (NessusWWW / LISTEN). :contentReference[oaicite:3]{index=3}

## Key findings (top items)
> These are highest-value observations from the scan output; full raw output is available in `sample_report_127.0.0.1.txt`.

1. Nessus web server active/listening on port **8834** (local web UI). :contentReference[oaicite:4]{index=4}  
2. Web servers detected: **Apache** and **nginx** installed.   
3. **OpenSSL** present (multiple versions indicated, e.g., 3.4.0 and 3.0.16 in metadata). Review TLS config/ciphers.   
4. **PHP 8.4.4** detected — ensure it's up-to-date and configured securely. :contentReference[oaicite:7]{index=7}  
5. **PostgreSQL 17.4** components present (client/server packages detected). Confirm DB is not exposed unnecessarily. :contentReference[oaicite:8]{index=8}  
6. **OpenJDK / Java** runtime detected (JRE/JDK 21.x) — validate whether versions require updates.   
7. **libcurl / curl** packages present (libcurl 8.12.1). Verify whether any CVE affects installed version. :contentReference[oaicite:10]{index=10}  
8. Network connections: multiple established outbound TLS connections observed in netstat output. :contentReference[oaicite:11]{index=11}

> Note: The raw scan text contains many installed packages and plugin outputs. The repo includes the full `sample_report_127.0.0.1.txt` for evidence.

## Risk level — Overall
**Medium.**  
The presence of multiple server stacks (web servers, DB client packages, TLS libraries, and runtimes) increases attack surface. Some items (outdated packages, misconfigurations) could be high-risk if confirmed vulnerable. Recommend prioritizing patching and secure configuration review.

## Recommended actions (quick)
- Patch system packages (run OS package update / apt update & apt upgrade).  
- Review and harden TLS configuration for services using OpenSSL (disable weak ciphers; enforce TLS 1.2/1.3). :contentReference[oaicite:12]{index=12}  
- Ensure Nessus UI (port 8834) is access-controlled (bind to localhost only if remote access not needed). :contentReference[oaicite:13]{index=13}  
- Verify PHP, Apache, nginx, Java versions and apply vendor security patches.   
- Check database (PostgreSQL) exposure — ensure it is not listening on external interfaces unless required. :contentReference[oaicite:15]{index=15}  
- Run targeted CVE lookups for identified package versions and remediate critical CVEs first.

## Evidence files in this repository
- `sample_report_127.0.0.1.txt` — raw scan output (source). :contentReference[oaicite:16]{index=16}  
- `findings.txt` — concise list of findings (human-readable).  
- `mitigations.txt` — short fixes per finding.


# Recon Checklist

My personal process for the reconnaissance phase. This grows every time I learn a new technique or get burned by missing something.

## Passive recon (no direct contact with target)
- [ ] WHOIS lookup on domain
- [ ] DNS records (A, MX, TXT, NS) — `dig`, `nslookup`
- [ ] Subdomain enumeration — `subfinder`, `crt.sh` (certificate transparency logs)
- [ ] Search engine recon (Google dorking) for exposed files, login pages, error messages
- [ ] Check for public code repos (GitHub) belonging to the org — leaked secrets, internal hostnames

## Active recon (direct contact with target)
- [ ] Port scan — `nmap -sC -sV -p- <target>` for full picture, `-sS` for stealth/speed when needed
- [ ] Service version identification — note exact versions for known-CVE lookup later
- [ ] Web recon (if HTTP/S open):
  - [ ] Directory/file brute force — `gobuster`, `ffuf`
  - [ ] Identify CMS/framework — `whatweb`, `wappalyzer`
  - [ ] Check `robots.txt`, `sitemap.xml`
- [ ] SMB/NetBIOS enum if 139/445 open — `enum4linux`, `smbclient -L`
- [ ] SNMP check if 161 open — default community strings

## After recon — before moving to exploitation
- [ ] List every open port + service + version in one place (table)
- [ ] Cross-reference versions against known CVEs (`searchsploit`, NVD)
- [ ] Note anything unusual (non-standard ports, odd banners, multiple web apps on same host)

---
*Last updated: (update this each time you revise)*

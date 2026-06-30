# Personal Cybersecurity Lab — Task 2

## Objective
Build a safe, isolated cybersecurity practice environment consisting of an attacker machine and a vulnerable target application, with verified connectivity and traffic-analysis tooling in place. This lab serves as the foundation for future tasks such as vulnerability assessment, web application testing, exploitation practice, and incident response.

## Architecture

| Component | Details |
|---|---|
| Attacker Machine | Kali Linux (VirtualBox VM) |
| Target Application | OWASP Juice Shop (Docker container, port 3000) |
| Network Adapter | Adapter 1 — NAT |
| Target Isolation | Docker bridge network on localhost |
| Validation Tools | Nmap, Burp Suite Community Edition, Wireshark |

**Note on design choice:** the original lab guide outlines a two-VM setup with NAT + Host-Only adapters. In this build, the target was deployed as a Docker container inside the Kali VM itself instead of a separate Host-Only segmented VM, due to host resource constraints. This still satisfies the core lab requirements — an isolated, intentionally vulnerable target reachable from the attacker machine, with full traffic-analysis validation.

## Setup Steps

1. Deployed Kali Linux as a VirtualBox VM with a NAT-attached network adapter.
2. Updated the system and created lab working directories.
3. Installed Docker and deployed OWASP Juice Shop:
```bash
   sudo apt install -y docker.io
   sudo systemctl enable --now docker
   sudo docker pull bkimminich/juice-shop
   sudo docker run -d -p 3000:3000 --name juice bkimminich/juice-shop
```
4. Verified connectivity with Nmap:
```bash
   nmap -sV -p 3000 localhost
```
5. Validated the target via browser, Burp Suite (proxy interception), and Wireshark (packet capture).

## Folder Structure

.
├── evidence/
│   ├── vm-info/        → network configuration (ip a output)
│   ├── connectivity/   → Nmap scan results
│   ├── juice-shop/     → target application screenshots
│   ├── burp/           → Burp Suite intercept screenshots
│   └── wireshark/      → Wireshark capture screenshots
├── pcaps/               → saved .pcapng packet capture file
├── report/               → Full Lab Build Report (.docx)
└── README.md

## Evidence Summary

- **Network Configuration** — confirmed NAT IP assignment via `ip a`
- **Connectivity** — Nmap scan confirmed port 3000 open and serving HTTP
- **Target Application** — Juice Shop homepage accessible at `localhost:3000`
- **Burp Suite** — intercepted live HTTP requests between browser and application
- **Wireshark** — captured and saved TCP traffic on the loopback interface

## Tools Used

- VirtualBox
- Kali Linux
- Docker
- OWASP Juice Shop
- Nmap
- Burp Suite Community Edition
- Wireshark

## Status

Lab environment built, validated, and documented. Ready for the next phase: vulnerability assessment and web application security testing.

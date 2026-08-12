---
name: github-repo-management
description: Expert guidance and automated standards for managing GitHub repositories, project directory layouts, security secret prevention, README maintenance, release strategies, and git workflows for cybersecurity homelabs and software projects.
---

# GitHub Repository & Lab Management Skill

This skill provides expert workflows and operational standards for creating, structuring, updating, and maintaining GitHub repositories—with special focus on cybersecurity homelabs (like Wazuh SOC labs), detection engineering repos, and general development projects.

## Core Capabilities & Standards

### 1. Repository Structure & Hierarchy
When initializing or refactoring a security/development repository, enforce standard directory organization:

```text
repository-root/
│
├── README.md                 # Primary documentation, architecture diagrams, status
├── .gitignore                # Security-focused exclusion rules
├── LICENSE                   # Open-source license (MIT, Apache 2.0, etc.)
│
├── docs/                     # Detailed guides, architecture notes, investigation logs
├── configs/                  # Sanitized configuration templates (.example extension)
│   ├── wazuh/                # ossec.conf.example, local_rules.xml
│   └── sysmon/               # sysmonconfig.xml.example
│
├── scripts/                  # Automated setup, verification, and helper scripts
│   ├── windows/              # PowerShell automation scripts
│   └── ubuntu/               # Bash setup & maintenance scripts
│
└── detections/               # Custom rules, decoders, and SIGMA mappings
    ├── rules/                # XML / YARA / SIGMA detection rules
    └── decoders/             # Custom log decoders
```

---

### 2. Secret & Telemetry Leak Prevention (Git Hygiene)

**CRITICAL RULE**: Never commit real authentication keys, private certificates, or sensitive log files containing actual user passwords or tokens.

#### Required `.gitignore` Patterns:
- **Authentication Keys**: `client.keys`, `*.key`, `*.pem`, `*.pfx`, `*.crt`, `*.cer`, `*.jks`
- **Secrets & Credentials**: `.env`, `secrets.yml`, `passwords.txt`, `credentials.json`
- **Install Packages & VMs**: `wazuh-install-files.tar`, `*.iso`, `*.ova`, `*.vmdk`, `*.qcow2`
- **Raw Telemetry & Dumps**: `alerts.json`, `archives.json`, `*.evtx`, `*.pcap`, `*.log`

#### Sanitization Guidelines:
- Use placeholder values in committed configs (e.g., `<address>WAZUH_MANAGER_IP</address>` or `<key>AGENT_KEY_PLACEHOLDER</key>`).
- Always suffix sample config files with `.example` (e.g., `ossec.conf.example`, `sysmonconfig.xml.example`).

---

### 3. README & Technical Documentation Standard

A top-tier GitHub README must contain:
1. **Title & Summary**: Clear 1-2 sentence overview of the project.
2. **Current Lab Architecture Diagram**: Mermaid flowcharts and ASCII layout visualizing network/host layout.
3. **Telemetry & Detection Flow**: Step-by-step pipeline from endpoint event collection -> decoder -> rule -> alert -> dashboard.
4. **Environment Specification Table**: Version numbers, IPs (internal lab ranges), OS versions, listening ports.
5. **Phase Progress / Roadmap Checklist**: Interactive markdown checklists (`[x]` vs `[ ]`) showing completed vs future milestones.
6. **Troubleshooting & Verification Commands**: Exact PowerShell & Bash snippet blocks to verify services, connectivity, and status.

---

### 4. Git Commit & Release Workflow

#### Commit Message Convention:
Follow Conventional Commits for clean history:
- `feat(detection): add custom rule for suspicious powershell execution`
- `docs(readme): update SCA compliance score and CIS benchmark details`
- `fix(agent): update manager IP address placeholder in ossec.conf.example`
- `chore(gitignore): add rules for evtx and pcap file exclusions`

#### Branch Strategy:
- `main`: Production-ready, sanitized documentation and stable configuration scripts.
- `feature/<name>` or `lab/phase-<N>`: Active work (e.g. `feature/sysmon-integration`, `lab/phase-6-fim`).

---

### 5. Repository Maintenance Checklist

When performing regular updates on a GitHub repo:
- [ ] Run secret scan check before pushing (`git status` review).
- [ ] Update `README.md` project status section and roadmap progress bar.
- [ ] Verify all file paths in documentation are relative or use markdown links.
- [ ] Ensure scripts have clear usage instructions and parameter defaults.


# ðŸš€ Cybersecurity Grandmaster Bootcamp

**Phase 0: LAB SETUP â€“ â€œThe War Roomâ€**  
Welcome to your first step in becoming a cybersecurity grandmaster. This phase sets up your cyber lab environment.

---

## ðŸ“š Table of Contents

- [ðŸŽ¯ Objectives](#-objectives)
- [ðŸ§± Host Machine Requirements](#-host-machine-requirements)
- [ðŸ§° Virtualization Stack](#-installation-of-virtualization-stack)
- [ðŸ–¥ï¸ VM Setup](#ï¸-vm-setup)
- [ðŸŒ Network Configuration](#-network-configuration)
- [ðŸ› ï¸ Core Tools Installation](#ï¸-core-tools-installation)
- [ðŸŽ¨ Visualization & Notes](#-visualization--notes)
- [ðŸ” Self-Test Checklist](#-self-test-checklist)
- [ðŸ§ª Final Lab](#-final-lab-hello-hacker)

---

## ðŸŽ¯ Objectives

| Goal | Description |
|------|-------------|
| ðŸŽ›ï¸ Hypervisor setup | Virtualize all OS environments (Windows, Linux, AD, Kali) |
| ðŸ› ï¸ Tool installation | All offensive/defensive tools installed & verified |
| ðŸ” Network simulation | Simulate real LANs, VLANs, AD domains |
| ðŸ”„ Snapshots & rollback | Enable quick resets after destructive testing |
| ðŸ§ª Self-Test | Validate system health and interconnectivity |

---

## ðŸ§± Host Machine Requirements

| Resource | Minimum | Recommended |
|---------|---------|-------------|
| CPU | 4 cores | 8+ cores |
| RAM | 8 GB | 16â€“32 GB |
| Storage | 100 GB free | 250+ GB SSD |
| OS | Windows 10/11 Pro or Linux | Any |
| Virtualization | Enabled in BIOS | KVM, Hyper-V, or VMware Workstation Pro |

---

## ðŸ§° Installation of Virtualization Stack

### ðŸ”¸ Option 1: VMware Workstation Pro (Preferred)
- Best for Windows hosts  
- [Download trial](https://www.vmware.com/products/workstation-pro.html)

### ðŸ”¹ Option 2: VirtualBox
- Cross-platform & free  
- [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)

### ðŸ”¸ Option 3: Proxmox VE (Advanced)
- Bare-metal hypervisor  
- Real VLAN and PXE boot simulations  
- [Proxmox ISO](https://www.proxmox.com/en/downloads)

---

## ðŸ–¥ï¸ VM Setup

| VM | OS | Use |
|----|----|-----|
| ðŸ›¡ï¸ Kali Linux | Latest | Attacker tools |
| ðŸªŸ Windows 10 | Pro | Target workstation |
| ðŸ¢ Windows Server 2019 | Std | AD Domain Controller |
| ðŸ§ Ubuntu Server | 22.04 | Web + SIEM |
| ðŸ§± Metasploitable2 | Vulnerable machine |
| ðŸ¬ JuiceShop | Web security lab |
| ðŸ§ª REMnux | Malware analysis |
| ðŸ§° Security Onion | Network defense stack |

```bash
# For Linux Hosts
sudo apt update
sudo apt install virtualbox virtualbox-ext-pack -y
```

---

## ðŸŒ Network Configuration

### ðŸ’¡ Network Types:
- Host-Only â€“ Isolated lab
- NAT â€“ Internet access for updates
- Internal â€“ For AD / domain setups
- Bridged â€“ Attack from your LAN

### ðŸ”Œ Sample Lab Topology

```
                +------------------+
                |   Kali Linux     |
                |  (Attacker)      |
                +--------+---------+
                         |
                   Host-Only Switch
                         |
          +--------------+-------------+
          |                            |
+-------------------+        +------------------+
| Win10 Workstation |        | Windows Server   |
| (victim)          |        | (DC: corp.local) |
+-------------------+        +------------------+
```

---

## ðŸ› ï¸ Core Tools Installation

### Offensive Tools
Install:
`nmap`, `netcat`, `msfconsole`, `impacket`, `burpsuite`, `wireshark`, `hydra`, `john`, `crackmapexec`, `kerbrute`

```bash
git clone https://github.com/SecureAuthCorp/impacket
git clone https://github.com/byt3bl33d3r/CrackMapExec
```

### Defensive Tools
`zeek`, `suricata`, `wazuh`, `velociraptor`, `securityonion`, `osquery`, `sysmon`

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
```

### Malware Analysis (REMnux)
```bash
wget -qO- https://REMnux.org/get | bash
```

---

## ðŸŽ¨ Visualization & Notes

Recommended tools for journaling and documentation:

- Draw.io â€“ Network & attack maps
- Obsidian / Joplin â€“ Cyber Warrior Journal
- CherryTree â€“ Tree-based notetaking
- Doom Emacs *(Optional)*

### Folder Structure

```
CyberMastery/
â”œâ”€â”€ Playbooks/
â”œâ”€â”€ Notes/
â”œâ”€â”€ Tools/
â”œâ”€â”€ Reports/
â””â”€â”€ Labs/
```

---

## ðŸ” Self-Test Checklist

- âœ… Can Kali ping Windows VMs?
- âœ… AD domain controller running?
- âœ… PCAP capture working?
- âœ… Tools operational (`nmap`, `msfconsole`, `rpcclient`, etc.)?
- âœ… Snapshots taken and working?

---

## ðŸ§ª Final Lab: "Hello, Hacker"

### Task:
1. Launch Kali.
2. Scan Windows 10 with `nmap`.
3. Capture traffic in Wireshark.
4. Use `smbclient` or `impacket` to list shares.
5. Document your steps in Obsidian.

---

> âœ… **Next Phase:** [Phase 1 â€“ Systems & Networking Internals]

# 🚀 Cybersecurity Grandmaster Bootcamp

**Phase 0: LAB SETUP – "The War Room"**  
Welcome to your first step in becoming a cybersecurity grandmaster. This phase sets up your cyber lab environment.

---

## 📚 Table of Contents

- [🎯 Objectives](#objectives)
- [🧱 Host Machine Requirements](#host-machine-requirements)
- [🧰 Virtualization Stack](#installation-of-virtualization-stack)
- [🖥️ VM Setup](#vm-setup)
- [🌐 Network Configuration](#network-configuration)
- [🛠️ Core Tools Installation](#core-tools-installation)
- [🎨 Visualization & Notes](#visualization--notes)
- [🔍 Self-Test Checklist](#self-test-checklist)
- [🧪 Final Lab](#final-lab-hello-hacker)

---

## 🎯 Objectives

| Goal | Description |
|------|-------------|
| 🎛️ Hypervisor setup | Virtualize all OS environments (Windows, Linux, AD, Kali) |
| 🛠️ Tool installation | All offensive/defensive tools installed & verified |
| 🔐 Network simulation | Simulate real LANs, VLANs, AD domains |
| 🔄 Snapshots & rollback | Enable quick resets after destructive testing |
| 🧪 Self-Test | Validate system health and interconnectivity |

---

## 🧱 Host Machine Requirements

| Resource | Minimum | Recommended |
|---------|---------|-------------|
| CPU | 4 cores | 8+ cores |
| RAM | 8 GB | 16–32 GB |
| Storage | 100 GB free | 250+ GB SSD |
| OS | Windows 10/11 Pro or Linux | Any |
| Virtualization | Enabled in BIOS | KVM, Hyper-V, or VMware Workstation Pro |

---

## 🧰 Installation of Virtualization Stack

### 🔸 Option 1: VMware Workstation Pro (Preferred)
- Best for Windows hosts  
- [Download trial](https://www.vmware.com/products/workstation-pro.html)

### 🔹 Option 2: VirtualBox
- Cross-platform & free  
- [Install VirtualBox](https://www.virtualbox.org/wiki/Downloads)

### 🔸 Option 3: Proxmox VE (Advanced)
- Bare-metal hypervisor  
- Real VLAN and PXE boot simulations  
- [Proxmox ISO](https://www.proxmox.com/en/downloads)

---

## 🖥️ VM Setup

| VM | OS | Use |
|----|----|-----|
| 🛡️ Kali Linux | Latest | Attacker tools |
| 🪟 Windows 10 | Pro | Target workstation |
| 🏢 Windows Server 2019 | Std | AD Domain Controller |
| 🐧 Ubuntu Server | 22.04 | Web + SIEM |
| 🧱 Metasploitable2 | Vulnerable machine |
| 🍬 JuiceShop | Web security lab |
| 🧪 REMnux | Malware analysis |
| 🧰 Security Onion | Network defense stack |

```bash
# For Linux Hosts
sudo apt update
sudo apt install virtualbox virtualbox-ext-pack -y
```

---

## 🌐 Network Configuration

### 💡 Network Types:
- Host-Only – Isolated lab
- NAT – Internet access for updates
- Internal – For AD / domain setups
- Bridged – Attack from your LAN

### 🔌 Sample Lab Topology

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

## 🛠️ Core Tools Installation

### Offensive Tools
Install: `nmap`, `netcat`, `msfconsole`, `impacket`, `burpsuite`, `wireshark`, `hydra`, `john`, `crackmapexec`, `kerbrute`

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
wget -qO- https://remnux.org/get | bash
```

---

## 🎨 Visualization & Notes

Recommended tools for journaling and documentation:

- Draw.io – Network & attack maps
- Obsidian / Joplin – Cyber Warrior Journal
- CherryTree – Tree-based notetaking
- Doom Emacs *(Optional)*

### Folder Structure

```
CyberMastery/
├── Playbooks/
├── Notes/
├── Tools/
├── Reports/
└── Labs/
```

---

## 🔍 Self-Test Checklist

- ✅ Can Kali ping Windows VMs?
- ✅ AD domain controller running?
- ✅ PCAP capture working?
- ✅ Tools operational (`nmap`, `msfconsole`, `rpcclient`, etc.)?
- ✅ Snapshots taken and working?

---

## 🧪 Final Lab: "Hello, Hacker"

### Task:
1. Launch Kali.
2. Scan Windows 10 with `nmap`.
3. Capture traffic in Wireshark.
4. Use `smbclient` or `impacket` to list shares.
5. Document your steps in Obsidian.

---

> ✅ **Next Phase:** [Phase 1 – Systems & Networking Internals]


 
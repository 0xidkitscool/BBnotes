# 🐛 Bug Bounty Toolkit 
*A curated list of tools and techniques for effective bug hunting*

---

## 📖 Table of Contents
- [🕵️ Fuzzing & Recon](#-fuzzing--recon)
- [🔍 Vulnerability Testing](#-vulnerability-testing)
- [📝 Note-Taking](#-note-taking)
- [⚙️ Automation](#️-automation)
- [💡 Contributing](#-contributing)

---

## 🕵️ Fuzzing & Recon

### Domain Enumeration
| Tool | Description | Installation |
|------|-------------|--------------|
| 🚀 **amass** | Subdomain enumeration via OSINT | `Arch: pacman -S amass, Debian: apt install amass` |
| 🌐 **sublist3r** | Fast subdomains enumeration tool | `Arch: pacman -S sublist3r, Debian: apt install sublist3r` |
| 🔍 **subfinder** | Subdomain discovery with multiple sources | `Arch: pacman -S subfinder, Debian: apt install subfinder` |

### Directory Fuzzing
| Tool | Description | Installation |
|------|-------------|--------------|
| 📂 **dirbuster** | Classic directory brute-forcing tool | `Arch: pacman -S dirbuster, Debian: apt install dirbuster` |
| ⚡ **ffuf** | Fast web fuzzer written in Go | `Arch: pacman -S ffuf, Debian: apt install ffuf` |

---

## 🔍 Vulnerability Testing

### Core Toolkit
🛡️ **Burp Suite Pro** - *Industry-standard web vulnerability scanner*  
🔑 Features:
- Intercepting proxy
- Automated scanning
- Advanced manual testing tools
- [Official Website](https://portswigger.net/burp/pro)

---

## 📝 Note-Taking

### Knowledge Management
| Tool | Description | Link |
|------|-------------|------|
| 🧠 **Obsidian** | Markdown-based knowledge base | [obsidian.md](https://obsidian.md) |
| 📒 **CherryTree** | Hierarchical note-taking application | [giuspen.com/cherrytree](https://www.giuspen.com/cherrytree) |

---

## ⚙️ Automation

🤖 **Osmedeus** - *All-in-one reconnaissance automation*  
```bash
docker pull osmedeus/osmedeus:latest

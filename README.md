# 🔥 Firewall Rule Engine & Conflict Analyzer

> A high-performance firewall rule parser, conflict detector, and ruleset optimizer built in V for iptables and nftables configurations.

[![Author](https://img.shields.io/badge/Made%20by-cyber--atharv-00ffcc?style=flat-square&logo=github)](https://github.com/cyber-atharv)
[![V Language](https://img.shields.io/badge/V-0.5+-5D87BF?style=flat-square&logo=v&logoColor=white)](https://vlang.io)
[![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)

---

## 📌 What is a Firewall Rule Conflict?

Firewall configurations often grow over time into hundreds of complex rules. A common security bug occurs when an earlier rule accidentally overrides (or "shadows") a later rule, or when duplicate and contradictory access policies create hidden security loopholes.

This tool, built by **cyber-atharv**, parses firewall rulesets (`iptables` and `nftables`), builds a unified evaluation tree, and identifies:
- **Shadowed Rules:** Rules that will never be reached because a previous rule already matched all packets.
- **Contradictory Rules:** Rules where one policy permits traffic that another policy blocks.
- **Redundancies & Dead Weight:** Inefficient rules that can be merged (e.g. combining separate port rules into one).
- **Security Hardening Gaps:** Missing anti-spoofing filters, lack of connection tracking (`conntrack`), or unrestricted ICMP traffic.

---

## ✨ Key Features

- **Unified Rule Parser:** Seamlessly reads standard `iptables-save` and `nft list ruleset` outputs.
- **Deep Conflict Detection:** Automatically flags rule order anomalies, shadowed blocks, and permission leaks.
- **Automatic Rule Optimizer:** Recommends port consolidation and reordering for maximum packet processing speed.
- **Hardened Ruleset Generator (`harden`):** Generates clean, production-ready default-deny rulesets with anti-spoofing and rate limiting enabled.
- **Rule Diff Engine (`diff`):** Compares two firewall configurations to spot changes before deploying updates.

---

## 🚀 Quick Start & Usage

### 1. Build and Install
```bash
cd firewall-rule-engine
# Using the install script
./install.sh
# Or compile directly with V:
v -prod -o fwrule .
```

### 2. Examples

#### 🔹 Analyze a firewall configuration for bugs
```bash
fwrule analyze my_firewall.rules
```

#### 🔹 Generate a baseline hardened firewall
```bash
fwrule harden --services ssh,http,https --iface eth0 --format iptables
```

#### 🔹 Compare two firewall rulesets
```bash
fwrule diff prod_rules.v1 prod_rules.v2
```

---

## 🧠 Why I Built This

Misconfigurations in network firewalls are among the most frequent root causes of network breaches. Writing a rule parser and conflict detector helped me understand how packet filtering engines evaluate network criteria sequentially and how to design clean "Zero-Trust / Default-Deny" firewall architectures.

---

## 📜 Author & License

- **Author:** [cyber-atharv](https://github.com/cyber-atharv)
- **License:** Open source under the MIT / AGPL License.

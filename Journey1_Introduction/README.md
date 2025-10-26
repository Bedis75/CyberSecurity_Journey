# Journey 1 — Introduction to Cybersecurity

> 📘 This README summarizes everything I learned in **Module 1: Introduction to Cybersecurity** from the *Cisco Junior Cybersecurity Analyst* course and my first **TryHackMe** rooms. It’s written in a simple, detailed, and beginner-friendly way — so I can understand everything clearly later without returning to the course.

---

## 🧠 What Is Cybersecurity?

Cybersecurity is the practice of protecting computers, networks, and data from attacks or unauthorized access. Its main goals are represented by the **CIA triad**:

* **Confidentiality:** Only authorized people can see the data.
* **Integrity:** The data stays correct and unchanged.
* **Availability:** The systems and data are accessible when needed.

Cybersecurity is not just about installing antivirus software — it’s a complete process that includes **people, policies, and technologies** working together to reduce risks.

---

## 🌍 1.1 The World of Cybersecurity

This part introduced the world of digital threats and how cybersecurity protects everything connected to the internet.

### 🔐 Why Cybersecurity Matters

Every organization stores valuable data — like customer info, passwords, or financial transactions. Hackers constantly try to steal or destroy it. Cybersecurity ensures safety, privacy, and business continuity.

### 👥 Main Cybersecurity Roles

#### 🟥 Red Team — *Attackers (Ethical Hackers)*

* Their job is to **simulate real cyberattacks** to find weaknesses before real hackers do.
* They use hacking tools, social engineering, and penetration testing.
* Example: A red team might try to hack a company’s login system to see if it’s secure.

#### 🟦 Blue Team — *Defenders*

* They **monitor networks, detect intrusions**, and respond to attacks.
* Use tools like firewalls, intrusion detection systems (IDS), and security information and event management (SIEM).
* Example: A blue team member investigates why an employee’s computer is communicating with a suspicious server.

#### 🟨 Incident Responders

* Specialists who act when an attack happens.
* Their job: stop the attack, minimize damage, and recover systems.

#### ⚖️ Governance, Risk, and Compliance (GRC) Teams

* They make sure the organization follows **laws, regulations, and security standards**.
* They define security policies, risk management strategies, and training.

---

## 🏢 1.2 Organizational Data

Organizations collect and store many kinds of data. Not all data is equal — some are public, some are private.

### 🧩 Types of Organizational Data

* **Public data:** Available to everyone (e.g., company website content).
* **Internal data:** Used inside the company (e.g., internal reports).
* **Confidential data:** Sensitive info (e.g., employee salaries, client data).
* **Restricted data:** Highly secret (e.g., encryption keys, classified projects).

### 📦 Why Data Classification Matters

Classifying data helps decide **how it should be protected**:

* Public data may not need encryption.
* Confidential and restricted data must be encrypted, have access controls, and strict permissions.

---

## 💾 1.3 What Was Taken?

When a cyberattack happens, understanding what was stolen is key to knowing how serious it is.

### 🔍 Common Types of Stolen Data

* **Personal Data:** Names, emails, or Social Security numbers.
* **Financial Data:** Credit card details, bank records.
* **Credentials:** Usernames, passwords, or tokens.
* **Intellectual Property:** Research, patents, product designs.
* **System Data:** Server configurations, internal IPs, and logs.

### ⚠️ Impact of a Breach

* Loss of customer trust.
* Financial loss due to fines or downtime.
* Exposure of trade secrets.
* Damage to the company’s reputation.

### 🧰 Response Steps

1. Detect the incident.
2. Preserve evidence (logs, screenshots).
3. Contain and fix vulnerabilities.
4. Inform authorities and affected users.

---

## 🕵️‍♂️ 1.4 Cyber Attackers

Attackers are categorized based on their intentions.

### ⚪ White Hat (Ethical Hackers)

* Work legally with permission to test systems.
* Goal: Find weaknesses so companies can fix them.
* Example: A white hat discovers a bug and reports it to the company.

### ⚫ Black Hat (Criminal Hackers)

* Hack systems illegally to steal, destroy, or sell data.
* Motivations: money, revenge, politics.
* Example: A hacker steals credit card data and sells it online.

### ⚫⚪ Gray Hat (In Between)

* May not have bad intentions but still break rules.
* Example: Someone finds a flaw and reveals it publicly instead of reporting it privately.

---

## ⚔️ 1.5 Cyberwarfare

Cyberwarfare happens when governments or military groups launch cyberattacks to harm another nation.

### 🎯 Goals

* Steal intelligence or classified information.
* Shut down critical infrastructure (power plants, hospitals, banks).
* Spread misinformation to create panic.

### 🧠 Examples

* Attacks on election systems or power grids.
* State-sponsored hacking groups (known as APTs — Advanced Persistent Threats).

Cyberwarfare is serious because it can affect millions of people and cause economic damage without a single bullet being fired.

---

## 💻 TRYHACKME — My First Labs

I practiced cybersecurity concepts in real environments using **TryHackMe**, a platform that provides guided virtual labs.

---

### 1️⃣ Offensive Security Intro

**Goal:** Learn how ethical hackers (red teamers) attack systems legally.

**What I Learned:**

* The difference between **ethical hacking** and **illegal hacking**.
* The 5 main phases of ethical hacking:

  1. **Reconnaissance:** Gather information about the target.
  2. **Scanning:** Identify open ports and services.
  3. **Exploitation:** Use vulnerabilities to gain access.
  4. **Privilege Escalation:** Get higher-level access.
  5. **Post-Exploitation:** Maintain access or extract data.

**Main Takeaway:** I learned to always work within permission boundaries and to understand how attackers think — so I can defend better.

---

### 2️⃣ Defensive Security Intro

**Goal:** Understand how blue teamers defend against attacks.

**What I Learned:**

* How a Security Operations Center (SOC) monitors systems 24/7.
* The importance of **logs** — records that show what happened on a system.
* Use of **SIEM tools** to collect and analyze data from multiple sources.
* The **incident response process:** detect → analyze → contain → eradicate → recover.

**Main Takeaway:** Defense is about visibility and speed — you must detect attacks quickly before they spread.

---

### 3️⃣ Search Skills

**Goal:** Learn how to find cybersecurity information efficiently.

**What I Learned:**
The room introduced websites and resources to help find tools, documentation, and vulnerabilities. Here are the most useful ones:

#### 🔍 General Search Tips

* Use **site:** filters (e.g., `site:docs.python.org socket`) to search in a specific site.
* Use **quotes** for exact matches (e.g., “SQL injection prevention”).

#### 🌐 Recommended Websites

| Website                                                                                     | Purpose                                                                                                                                  |
| ------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| [Shodan](https://www.shodan.io)                                                             | Search engine for internet-connected devices (servers, webcams, routers, IoT). Use it to discover exposed services and software banners. |
| [Censys](https://censys.io)                                                                 | Internet-wide scanner and search engine focused on hosts and TLS certificates; useful for discovering HTTPS/TLS misconfigurations.       |
| [Linux Manual Pages (man pages)](https://man7.org/linux/man-pages/)                         | Official, built-in documentation for Linux commands and system calls. Access with `man <command>` on any Linux system.                   |
| [TryHackMe AttackBox](https://tryhackme.com/attackbox)                                      | A browser-accessible Linux machine used in TryHackMe labs. Start the AttackBox to run commands and follow lab tasks without local setup. |
| [Microsoft Docs (Windows)](https://learn.microsoft.com)                                     | Official Microsoft product documentation and technical guidance for Windows and other Microsoft technologies.                            |
| [Product Documentation (vendor docs)](https://en.wikipedia.org/wiki/Software_documentation) | Official manuals and guides published by software vendors. Always consult vendor docs for configuration and secure defaults.             |
| [VirusTotal](https://www.virustotal.com)                                                    | Upload files or URLs to get multi-engine antivirus scans and community analysis to check for known malware.                              |
| [Have I Been Pwned](https://haveibeenpwned.com)                                             | Search whether an email or password has appeared in known data breaches; useful for breach detection and remediation.                    |
| [CVE (MITRE)](https://cve.mitre.org)                                                        | The Common Vulnerabilities and Exposures catalog — search CVE IDs for authoritative vulnerability descriptions.                          |
| [Exploit Database (Exploit-DB)](https://www.exploit-db.com/)                                | Repository of proof-of-concept exploits and vulnerability write-ups (use only in authorized test environments).                          |
| [GitHub](https://github.com)                                                                | Code hosting platform where security tools, scripts, and research are published. Check README files and license before using tools.      |

**Main Takeaway:** I learned how to search smarter, not harder — using the right keywords and platforms can save hours of investigation.

**Abbreviations explained:**

* **PoC** = *Proof of Concept* — a small demo that shows a vulnerability can be exploited. Always use PoCs responsibly.
* **CVE** = *Common Vulnerabilities and Exposures* — a standardized ID system for known vulnerabilities.
* **NVD** = *National Vulnerability Database* — a U.S. government database that provides additional details and severity scores for CVEs.
* **SIEM** = *Security Information and Event Management* — systems that collect, store, and analyze log data to detect suspicious activity.

---

## 🧩 Summary

---

## 🧩 Summary

By completing Module 1 and these three rooms, I built a strong foundation:

* I now understand **how attackers think** and **how defenders respond**.
* I can classify data and know what makes it sensitive.
* I practiced both offensive and defensive concepts legally.
* I developed research and analysis skills for real-world cybersecurity work.

---

**Next Steps:**
Continue to **Module 2** of the Cisco course and explore more practical labs on TryHackMe (network fundamentals, threat detection, and Linux privilege escalation).

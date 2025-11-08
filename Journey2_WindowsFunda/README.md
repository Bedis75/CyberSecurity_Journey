# Journey 2 — Linux & Windows Fundamentals (Comprehensive room-based README) 💻

> 🎯 **Goal:** When you read this file you should not need to reopen the TryHackMe rooms. This README explains, in detail, every concept, command, and procedure covered in the five rooms you completed: **Linux Fundamentals Part 1**, **Windows Fundamentals 1, 2, 3**, and **Active Directory Basics**. The content is expanded into clear, memorable explanations and exercises.

-----

## 📚 How to Use This Document

Read one room at a time. Each room section contains: what it teaches, why it matters, concrete commands/examples, common outputs and how to interpret them, and short exercises you can replay in the **AttackBox** or a **VM**.

> 💡 **Action:** When a command is shown, copy-paste it into the **AttackBox (Linux)** or into a **Windows VM** to reproduce outputs and practice.

-----

## 🐧 Linux Fundamentals Part 1

### What this room teaches (big picture)

Basic Linux concepts and daily commands so you can **navigate, inspect, and search** a Linux system. The focus is practical — the commands are the core skill.

### Core Concepts Explained

  * **Kernel vs Distribution:**
      * **Kernel** = core OS component that manages CPU, memory, devices.
      * **Distro** = kernel + system tools + package manager (**Ubuntu, Debian, Kali**…). You mostly interact with the distro’s userland tools.
  * **Shell (`bash`):** Command interpreter. You type commands, it runs them and returns output. Learning shell basics is essential.
  * **Users and root:** **root** is the superuser. Use `sudo` to run commands as root. Normal users have limited privileges.

### Filesystem Layout (What Each Folder Means)

| Folder | Description |
| :--- | :--- |
| `/` | Root of filesystem. |
| `/home` | Users’ personal folders. |
| `/etc` | System and service configuration files (e.g., `/etc/passwd`, `/etc/hosts`). |
| `/var` | Variable data (logs in `/var/log`). |
| `/usr`, `/usr/bin` | User programs and common executables. |
| `/bin`, `/sbin` | Essential binaries; `/sbin` often admin-only. |
| `/tmp` | Temporary files. |

### Essential Commands and Interpretation

| Command | Purpose | Example Output | Interpretation |
| :--- | :--- | :--- | :--- |
| `pwd` | Prints working directory. | `/home/bedis` | Current directory. |
| `whoami` | Current user. | `bedis` | The user you are currently logged in as. |
| `ls -la` | Lists files with **permissions**, owner, size, timestamp. | `-rw-r--r-- 1 bedis bedis 1234 Jul 1 12:00 notes.txt` | `*regular file -`, `owner bedis`, `group bedis`, `size 1234`. |
| `cat file.txt` | Print file content. | *(File content)* | Use `less file.txt` for paged view. |
| `head -n 10 file` / `tail -n 10 file` | First/last lines. | *(First/last 10 lines)* | Useful for quickly checking logs or configuration files. |
| `file filename` | Guess file type. | `ASCII text, ELF 64-bit executable` | Helps identify the nature of a file. |
| `stat file` | Metadata. | *(Detailed info)* | Shows size, permissions, and timestamps. |

### Searching Files & Contents

  * **Search filenames:** `find / -name 'secret.txt' 2>/dev/null`
      * **Tip:** `2>/dev/null` hides "Permission denied" errors.
  * **Search file contents recursively:** `grep -R "password" /etc 2>/dev/null`
      * **Tip:** `-n` adds line numbers to the output.
  * **Quick filename search:** `locate filename`
      * **Note:** Uses updated database; run `sudo updatedb` to refresh DB (if available).

### Shell Operators (Practical Use)

| Operator | Purpose | Example | Explanation |
| :--- | :--- | :--- | :--- |
| `>` | Write output to file (overwrite). | `echo hello > file.txt` | Overwrites `file.txt` with "hello". |
| `>>` | Append output to file. | `echo world >> file.txt` | Adds "world" to the end of `file.txt`. |
| `|` | Pipe: command1 output becomes command2 input. | `ps aux | grep ssh` | Filters the process list for processes with "ssh". |
| `&&` | Run next only if previous succeeded. | `mkdir test && cd test` | Creates `test` and then changes directory only if creation succeeded. |
| `||` | Run next only if previous failed. | `command1 || echo "failed"` | Runs `command1`; if it fails, prints "failed". |
| `$(command)` | Substitution stores output to variable. | `today=$(date +%F)` | Sets the variable `today` to today's date. |
| `2>&1` | Redirect stderr to stdout. | `command 2>&1 | less` | Pipes both normal output and errors to `less`. |
| `2>/dev/null` | Hide stderr. | `find / -name secret 2>/dev/null` | Hides permission errors. |

### Short exercises (AttackBox)

```bash
# Confirmation
pwd; whoami; ls -la

# Show distro info
cat /etc/os-release

# List some config files (find + pipe + head)
find / -maxdepth 3 -type f -name '*.conf' 2>/dev/null | head

# Write and read a file in /tmp
echo "hello" > /tmp/test && cat /tmp/test
```

-----

## 🪟 Windows Fundamentals 1

### What this room teaches (big picture)

Windows GUI basics, editions, the **NTFS filesystem**, the **System32** folder, user accounts and **UAC**, and process inspection with **Task Manager**.

### Windows Editions (Why it Matters)

  * **Home:** Consumer edition — limited management features (no Group Policy editor, limited BitLocker controls).
  * **Pro/Enterprise/Education:** Include **BitLocker**, **Group Policy**, **domain join** capabilities. Crucial for enterprise defense and attack.

### Key System Components

  * **C:\\Windows\\System32:** Stores OS binaries and DLLs required by Windows. Modifying files here can break the system.
  * **Task Manager (`Ctrl+Shift+Esc`):** Tabs include Processes, Performance, Users, Details, Services. Use to spot high-resource processes or right-click to **open file location** of a running binary.

### User Accounts & UAC

  * **UAC (User Account Control):** Separates admin consent from normal operation. Even admin accounts operate with **filtered tokens** until an elevation prompt is accepted.
  * **NTFS Permissions:** Uses **ACLs (Access Control Lists)** for fine-grained permissions. `icacls <path>` displays permissions and inheritance.
  * **Commands:** `whoami /groups`, `net user`.

### Short exercises (Windows VM)

```powershell
# In File Explorer, identify explorer.exe
Open C:\Windows\System32 and identify explorer.exe.

# Inspect token and group privileges
cmd
whoami /priv
whoami /groups

# Find the location of a running process
In Task Manager, find explorer.exe, right click -> Open file location.
```

-----

## ⚙️ Windows Fundamentals 2

### What this room teaches (big picture)

System Configuration (`msconfig`), UAC settings, **Computer Management**, **System Information**, **Resource Monitor**, **Command Prompt** basics and the **Registry**.

### System Utilities

  * **System Configuration (`msconfig`):** Used to disable startup items and debug boot problems.
  * **Computer Management (`compmgmt.msc`):** Central console for Disk Management, Event Viewer, Local Users and Groups, Shared Folders.
  * **System Information (`msinfo32` / `systeminfo`):**
      * `msinfo32` (GUI) lists hardware/software.
      * `systeminfo` (CLI) prints OS, uptime, and patch level.
  * **Resource Monitor (`resmon`):** Shows per-process **CPU, disk, network, and memory usage** — a deeper view than Task Manager.

### Command Prompt Essentials

| Command | Purpose |
| :--- | :--- |
| `ipconfig /all` | Network adapter details. |
| `netstat -ano` | Active connections with **PID** owner. |
| `tasklist` | Running processes and PIDs. |

### Registry Editor (`regedit`)

  * **Hives:** **HKLM** (HKEY\_LOCAL\_MACHINE - machine-wide settings), **HKCU** (HKEY\_CURRENT\_USER - current user settings).
  * **Tip:** Always **File → Export** keys to back up before experimenting.

### Short exercises (Windows VM)

```powershell
# Inspect startup programs
msconfig

# Inspect detailed resource usage
resmon

# Registry backup practice (safe, read-only)
In regedit, export HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

-----

## 🛡️ Windows Fundamentals 3

### What this room teaches (big picture)

Windows security controls: updates, **Windows Security (Defender)**, firewall, device security and **TPM**, **BitLocker** encryption, and **VSS (Volume Shadow Copy)**.

### Windows Security & Patching

  * **Windows Update:** **Quality updates** fix bugs/security; **Feature updates** add functionality. Patch management reduces attack surface.
  * **Windows Security (Defender):** App provides Virus & threat protection, Firewall & network protection, App & browser control, Device security. Check last scan and signature version.
  * **Firewall:** Blocks inbound by default. View rules with **Windows Defender Firewall with Advanced Security** or PowerShell `Get-NetFirewallRule`.

### Device Security & Encryption

  * **Device Security & TPM:** Shows Secure Boot and **TPM** presence. The **TPM (Trusted Platform Module)** stores keys securely.
  * **BitLocker basics:** Encrypts volumes. **Protectors** include TPM, PIN, Startup Key (USB), and **Recovery Key** (48-digit).

### Volume Shadow Copy Service (VSS)

  * **VSS:** Creates **snapshots** so backups can capture files in use. Threat actors often abuse VSS to steal credentials or files.
  * **VSS Commands:**
      * `vssadmin list shadows`: list snapshots.
      * `vssadmin create shadow /for=C:`: create a snapshot.

### BitLocker Commands

```powershell
manage-bde -status  # Check encryption state (Encryption Method, Percentage Encrypted).
manage-bde -protectors -get C: # List protectors and recovery password IDs.
```

### Short exercises (Windows VM)

```powershell
# Check encryption state
manage-bde -status

# Inspect Windows Security GUI
Open Windows Security app -> Virus & threat protection.

# List VSS snapshots
vssadmin list shadows
```

-----

## 🔑 Active Directory Basics

### What this room teaches (big picture)

Directory services and Windows domain fundamentals: AD roles and objects, user/computer management, **Group Policy**, and **Kerberos** authentication overview.

### Key AD Concepts

  * **Domain:** Collection of objects (users, computers) managed centrally.
  * **Domain Controller (DC):** Server that runs **AD DS** (Active Directory Domain Services) and the **KDC** (Key Distribution Center for Kerberos).
  * **Forest / Tree:** Forest is top-level collection of domains sharing schema; trees are domain hierarchies.
  * **OU (Organizational Unit):** Container for grouping objects and applying **GPOs**.

### AD Objects & Attributes

| Object Type | Key Attributes | Notes |
| :--- | :--- | :--- |
| **User** | `sAMAccountName` (legacy logon), `userPrincipalName` (UPN, e.g., `user@domain.local`), `objectSID`. | Users authenticate to the domain. |
| **Computer** | Represents a machine joined to the domain. | |
| **Groups** | Used to grant permissions to multiple users simultaneously. | Group scope matters for security. |

### Kerberos Simplified (The Authentication Flow)

Kerberos is the default authentication protocol for Active Directory.

1.  **AS-REQ:** Client authenticates to the **KDC** (on the DC).
2.  **AS-REP:** KDC returns a **TGT (Ticket Granting Ticket)** if credentials are valid.
3.  **TGS-REQ:** Client uses the TGT to request a **Service Ticket** for a target service (e.g., SMB/File Share).
4.  **TGS-REP:** KDC returns the Service Ticket.
5.  **Client → Service:** Client presents the Service Ticket to the service to access the resource.

*(Resource: [Kerberos video: https://www.youtube.com/watch?v=954RqKDFk7o\&t=103s](https://www.youtube.com/watch?v=954RqKDFk7o&t=103s))*

### Group Policy Basics

  * **Order of Application (LSDOU):** **Local → Site → Domain → OU**. Policies applied later in this order win on conflicts.
  * **GPO Uses:** Enforce password policies, deploy scripts, map drives, restrict settings.

### Managing Users & Computers

  * Use **Active Directory Users and Computers (ADUC)** GUI to create users, reset passwords, add to groups, and move objects into OUs.
  * **Commands (lab-limited):** `net user /domain`, `dsquery`, `dsadd`.

### Short exercises (AD lab)

```plaintext
# ADUC exercises
1. In ADUC create a test user.
2. Set password.
3. Add to a test group.

# Inspect user properties
Inspect attributes: sAMAccountName, userPrincipalName, memberOf.

# Kerberos steps (for memory recall)
Write in 4 lines the Kerberos steps: 
AS-REQ/AS-REP (TGT) -> TGS-REQ/TGS-REP (Service Ticket)
```

-----

## 🧠 Practical Memory Aids & Final Checklist

### Study Method

When you re-read: first read the **Key takeaways** for the room, then run **3 commands** from the **Short exercises** to reactivate muscle memory.

> 📝 **Tip:** Keep a Git repo (`journey-2`) with this `README` and a `notes/` folder: one `.md` per room where you paste command outputs you collected during labs.

### Final Checklist (Things you should be able to do)

| Domain | Key Skills |
| :--- | :--- |
| **Linux** | Navigate filesystem, read files, search text, combine commands with pipes and redirections. |
| **Windows** | Inspect processes/services, find key system files (`System32`), understand UAC tokens, use Resource Monitor and `msconfig`. |
| **Windows Security** | Explain BitLocker protectors and check status, find VSS snapshots, use Windows Security GUI. |
| **Active Directory** | Create a user in ADUC, read key attributes, explain Kerberos flow (**AS → TGT → TGS → Service**), and describe GPO application order (**LSDOU**). |
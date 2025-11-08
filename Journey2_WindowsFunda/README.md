Journey 2 — Linux & Windows Fundamentals (Comprehensive room-based README) 💻
Goal
When you read this file you should not need to reopen the TryHackMe rooms. This README explains, in detail, every concept, command, and procedure covered in the five rooms you completed: Linux Fundamentals Part 1, Windows Fundamentals 1, 2, 3, and Active Directory Basics. I kept strictly to the rooms’ scope and expanded the content into clear, memorable explanations and exercises.

How to use this document
Read one room at a time. Each room section contains: what it teaches, why it matters, concrete commands/examples, common outputs and how to interpret them, and short exercises you can replay in the AttackBox or a VM.

When a command is shown, copy-paste it into the AttackBox (Linux) or into a Windows VM to reproduce outputs and practice.

Linux Fundamentals Part 1
What this room teaches (big picture)
Basic Linux concepts and daily commands so you can navigate, inspect, and search a Linux system. The focus is practical — the commands are the core skill.

Core concepts explained
Kernel vs Distribution:

Kernel = core OS component that manages CPU, memory, devices.

Distro = kernel + system tools + package manager (Ubuntu, Debian, Kali…). You mostly interact with the distro’s userland tools.

Shell (bash): command interpreter. You type commands, it runs them and returns output. Learning shell basics is essential.

Users and root: root is the superuser. Use sudo to run commands as root. Normal users have limited privileges.

Filesystem layout (what each folder means)
/: root of filesystem.

/home: users’ personal folders.

/etc: system and service configuration files (e.g., /etc/passwd, /etc/hosts).

/var: variable data (logs in /var/log).

/usr, /usr/bin: user programs and common executables.

/bin, /sbin: essential binaries; /sbin often admin-only.

/tmp: temporary files.

Essential commands, outputs, and how to read them
Command	Purpose	Example Output	Interpretation
pwd	prints working directory.	/home/bedis	Current directory.
whoami	current user.	bedis	The user you are currently logged in as.
ls -la	lists files with permissions, owner, size, timestamp.	-rw-r--r-- 1 bedis bedis 1234 Jul 1 12:00 notes.txt	*regular file -, owner bedis, group bedis, size 1234.
cat file.txt	print file content.	(File content)	Use less file.txt for paged view.
head -n 10 file / tail -n 10 file	first/last lines.	(First/last 10 lines)	Useful for quickly checking logs or configuration files.
file filename	guess file type.	ASCII text, ELF 64-bit executable	Helps identify the nature of a file.
stat file	metadata.	(Detailed info)	Shows size, permissions, and timestamps.

Exporter vers Sheets

Searching files & contents
Search filenames: find / -name 'secret.txt' 2>/dev/null

Tip: 2>/dev/null hides permission errors.

Search file contents recursively: grep -R "password" /etc 2>/dev/null

Tip: -n adds line numbers to the output.

Quick filename search: locate filename

Note: Uses updated database; run sudo updatedb to refresh DB (if available).

Shell operators (practical use)
Operator	Purpose	Example	Explanation
>	write output to file (overwrite).	echo hello > file.txt	Overwrites file.txt with "hello".
>>	append output to file.	echo world >> file.txt	Adds "world" to the end of file.txt.
|	pipe: command1 output becomes command2 input.	ps aux | grep ssh	Filters the process list for processes with "ssh".
&&	run next only if previous succeeded.	mkdir test && cd test	Creates test and then changes directory only if creation succeeded.
||	run next only if previous failed.	command1 || echo "failed"	Runs command1; if it fails, prints "failed".
$(command)	substitution stores output to variable.	today=$(date +%F)	Sets the variable today to today's date (e.g., 2024-01-01).
2>&1	redirect stderr to stdout.	command 2>&1 | less	Pipes both normal output and errors to less.
2>/dev/null	hide stderr.	find / -name secret 2>/dev/null	Hides the "Permission denied" errors.

Exporter vers Sheets

Short exercises (AttackBox)
Bash

# Confirmation
pwd; whoami; ls -la

# Show distro info
cat /etc/os-release

# List some config files (find + pipe + head)
find / -maxdepth 3 -type f -name '*.conf' 2>/dev/null | head

# Write and read a file in /tmp
echo "hello" > /tmp/test && cat /tmp/test
Windows Fundamentals 1
What this room teaches (big picture)
Windows GUI basics, editions, the NTFS filesystem, the System32 folder, user accounts and UAC, and process inspection with Task Manager.

Windows editions (why it matters)
Home: Consumer edition — limited management features (no Group Policy editor, limited BitLocker controls).

Pro/Enterprise/Education: Include BitLocker, Group Policy, domain join capabilities. When defending or attacking enterprise environments, these features matter.

Desktop & Control Panel vs Settings
Settings is modern UI, Control Panel is legacy but still contains advanced options.

Key UI elements: Start Menu, Action Center, File Explorer, Taskbar.

NTFS basics & file permissions
NTFS uses ACLs (Access Control Lists) with fine-grained permissions.

Command: icacls <path> displays permissions and inheritance.

Ownership determines who can change permissions.

C:\Windows\System32
Stores OS binaries and DLLs required by Windows.

Modifying files here can break the system.

Use Task Manager → Right click → Open file location to inspect real binaries behind running processes.

User accounts & UAC
UAC (User Account Control) separates admin consent from normal operation: even admin accounts operate with filtered tokens until elevation.

Commands: whoami /groups, net user.

Task Manager
Open: Ctrl+Shift+Esc.

Tabs include: Processes, Performance, Users, Details, Services.

Use to spot high-resource processes, right-click to open file location, and to end tasks.

Short exercises (Windows VM)
PowerShell

# In File Explorer, identify explorer.exe
Open C:\Windows\System32 and identify explorer.exe.

# Inspect token and group privileges
cmd
whoami /priv
whoami /groups

# Find the location of a running process
In Task Manager, find explorer.exe, right click -> Open file location.
Windows Fundamentals 2
What this room teaches (big picture)
System Configuration (msconfig), UAC settings, Computer Management, System Information, Resource Monitor, Command Prompt basics and the Registry.

System Configuration (msconfig)
Used to disable startup items and debug boot problems. Useful during troubleshooting.

Changing UAC
Control Panel → User Accounts → Change User Account Control settings.

Lowering the slider reduces prompts but weakens security.

Computer Management (compmgmt.msc)
Central console: Disk Management, Event Viewer, Local Users and Groups, Shared Folders.

Disk Management shows partitions and volumes — do not alter the system disk unless in a safe lab VM.

System Information (msinfo32 and systeminfo)
msinfo32 (GUI) lists hardware and software environment.

systeminfo prints OS, uptime, and patch level.

Resource Monitor (resmon)
resmon shows per-process CPU, disk, network, and memory usage — deeper than Task Manager.

Command Prompt essentials
Command	Purpose
ipconfig /all	network adapter details.
netstat -ano	active connections with PID owner.
tasklist	running processes and PIDs.

Exporter vers Sheets

Registry Editor (regedit)
Hives: HKLM (HKEY_LOCAL_MACHINE - machine-wide settings), HKCU (HKEY_CURRENT_USER - current user settings).

Export keys to back up before experimenting (File → Export).

Short exercises (Windows VM)
PowerShell

# Inspect startup programs
msconfig

# Inspect detailed resource usage
resmon

# Registry backup practice (safe, read-only)
In regedit, export HKCU\Software\Microsoft\Windows\CurrentVersion\Run
Windows Fundamentals 3
What this room teaches (big picture)
Windows security controls: updates, Windows Security (Defender), firewall, device security and TPM, BitLocker encryption, and VSS (Volume Shadow Copy).

Windows Update
Quality updates fix bugs and security issues. Feature updates add functionality.

Patch management reduces the attack surface.

Windows Security (Defender)
App provides: Virus & threat protection, Firewall & network protection, App & browser control, Device security.

Check last scan and signature version.

Firewall & network protection
Windows Firewall blocks inbound by default.

Use Windows Defender Firewall with Advanced Security or PowerShell Get-NetFirewallRule to view rules.

Device Security & TPM
Device security shows Secure Boot and TPM presence.

TPM (Trusted Platform Module) stores keys securely; private key bytes are not exportable by design.

BitLocker basics
BitLocker encrypts volumes.

Protectors: TPM, PIN, Startup Key (USB), Recovery Key (48-digit).

Commands:

manage-bde -status: check encryption state.

manage-bde -protectors -get C:: list protectors and recovery password IDs (not the private key itself).

Volume Shadow Copy Service (VSS)
VSS creates snapshots so backups can capture files in use.

Commands:

vssadmin list shadows: list snapshots.

vssadmin create shadow /for=C:: create a snapshot.

Short exercises (Windows VM)
PowerShell

# Check encryption state
manage-bde -status

# Inspect Windows Security GUI
Open Windows Security app -> Virus & threat protection.

# List VSS snapshots
vssadmin list shadows
Active Directory Basics
What this room teaches (big picture)
Directory services and Windows domain fundamentals: AD roles and objects, user/computer management, Group Policy, and Kerberos authentication overview.

Key AD concepts
Domain: collection of objects (users, computers) managed centrally on Domain Controllers (DCs).

Domain Controller (DC): server that runs AD DS (Active Directory Domain Services) and KDC (Key Distribution Center for Kerberos).

Forest / Tree: forest is top-level collection of domains sharing schema; trees are domain hierarchies.

OU (Organizational Unit): container for grouping objects and applying GPOs.

AD objects & attributes
User attributes: sAMAccountName (legacy logon name), userPrincipalName (UPN, e.g., user@domain.local), objectSID.

Computer object: represents a machine joined to the domain.

Groups: used to grant permissions; group scope matters.

Kerberos simplified (remember this flow)
AS-REQ: client authenticates to KDC (on DC).

AS-REP: KDC returns TGT (Ticket Granting Ticket) if credentials valid.

TGS-REQ: client uses TGT to request a Service Ticket for a target service.

TGS-REP: KDC returns the Service Ticket.

Client → Service: client presents the Service Ticket to the service (e.g., SMB) to access it.

(Your Kerberos video: https://www.youtube.com/watch?v=954RqKDFk7o&t=103s — it visually explains TGT vs service tickets.)

Group Policy basics
Order of application (LSDOU): Local → Site → Domain → OU. Policies later in that order win on conflicts.

GPO uses: enforce password policies, deploy scripts, map drives, restrict settings.

Managing users & computers
Use Active Directory Users and Computers (ADUC) GUI to create users, reset passwords, add to groups, move objects into OUs.

Commands (lab-limited): net user /domain, dsquery, dsadd.

Short exercises (AD lab)
Plaintext

# ADUC exercises
1. In ADUC create a test user.
2. Set password.
3. Add to a test group.

# Inspect user properties
Inspect attributes: sAMAccountName, userPrincipalName, memberOf.

# Kerberos steps (for memory recall)
Write in 4 lines the Kerberos steps: 
AS-REQ/AS-REP (TGT) -> TGS-REQ/TGS-REP (Service Ticket)
Practical memory aids & study method
When you re-read: first read the Key takeaways for the room, then run 3 commands from the Short exercises to reactivate muscle memory.

Keep a Git repo journey-2 with this README and a notes/ folder: one .md per room where you paste command outputs you collected during labs.

Final checklist (things you should be able to do after reading once)
Linux: navigate filesystem, read files, search text, combine commands with pipes and redirections.

Windows: inspect processes/services, find key system files, understand UAC tokens, use Resource Monitor and msconfig.

Windows security: explain BitLocker protectors and check status, find VSS snapshots, use Windows Security GUI.

Active Directory: create a user in ADUC, read key attributes, explain Kerberos flow (AS → TGT → TGS → Service), and describe what a GPO does and where it applies (LSDOU).
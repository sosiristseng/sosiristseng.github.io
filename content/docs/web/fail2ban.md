---
title: Fail2ban
tags:
  - web
---

[fail2ban](https://wiki.archlinux.org/title/Fail2ban) scans log files (e.g. `/var/log/auth.log`) and bans IPs that show the malicious signs like too many authentication attempts, scanning for vulnerabilities, etc.

## Install

```sh
sudo apt update && sudo apt install fail2ban -y
```

Verify `fail2ban` active.

```sh
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

## Configure

Create a file `/etc/fail2ban/jail.local` to override the default settings like this,

```sh
sudo nano /etc/fail2ban/jail.local
```

```{filename="/etc/fail2ban/jail.local"}
[DEFAULT]
ignoreip = 127.0.0.1/8 ::1 192.168.0.0/16
bantime  = 1d
maxretry  = 5
findtime  = 1d
bantime.increment = true
bantime.factor    = 2
bantime.maxtime   = 16d

[sshd]
enabled  = true
backend  = systemd
port     = ssh
```

After file save, reload the settings

```sh
sudo fail2ban-client reload
```

## Management

How is `fail2ban` doing

```sh
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

You can see the log from the `sshd` service as a reference (started from the most recent events)

```sh
sudo journalctl -ru ssh.service | grep 'Failed password' | less
```

### Unban an address

Unban one IP address

```sh
sudo fail2ban-client set sshd unbanip 198.51.100.24
```

Unban all

```sh
sudo fail2ban-client unban --all
```

## Sources

- [Harden SSH Against Brute Force with fail2ban](https://www.centron.de/en/tutorials/harden-ssh-brute-force-fail2ban)
- [三個提升Server安全性的設定之Fail2ban](https://wehelp.tw/topic/5638781679960064)
- [Linux作業系統如何限制SSH在一段時間內的嘗試登入次數，來避免被暴力破解登入？](https://magiclen.org/fail2ban-ssh/)

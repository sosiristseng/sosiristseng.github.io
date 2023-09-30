---
title: Add signing keys to apt
draft: false
tags:
  - linux/ubuntu
---

> Use of `apt-key` is deprecated according to the [Debian manpage](https://manpages.debian.org/testing/apt/apt-key.8.en.html)

Here, we take adding signing keys for [[vivaldi]] browser as an example.

```sh
curl -fsSL https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/vivaldi-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/vivaldi-keyring.gpg] https://repo.vivaldi.com/archive/deb/ stable main" | sudo tee /etc/apt/sources.list.d/vivaldi.list > /dev/null
```

- Text key files (`.asc`) should be converted to binary ones (`.gpg`) using `gpg --dearmor`.
- In the apt list, use `[signed-by=/path/to/key.gpg]` to specify the location of the keyring.
- Use `echo <stuff> | sudo tee <file>` to add file content with sudo rights.
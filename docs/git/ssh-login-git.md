---
title: SSH login to GitHub and GitLab
draft: 
tags:
  - github
  - gitlab
  - ssh
  - git
---
## Generate a pair of SSH keys

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```

The SSH agent will ask you to enter a location to save the keys. e.g. `/home/user/.ssh/id_ed25519`. Passphrase is optional.
Then there will be two SSH key files:

- `~/.ssh/id_ed25519` is the *private key*. **Protect it at all costs.**
- `~/.ssh/id_ed25519.pub` is the *public key*.

> Using different keys for GitHub and GitLab access is more secure. However, the same pair of keys is used for this demonstration purposes.

## Add remote to the SSH settings

Edit `~/.ssh/config`

```sh
mkdir -p ~/.ssh
touch ~/.ssh/config
chmod 600 ~/.ssh/config
nano ~/.ssh/config
```

Add the following content to set the *private key* as the IdentityFile.

```txt title="~/.ssh/config"
Host GitHub
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519

Host GitLab
  HostName gitlab.com
  IdentityFile ~/.ssh/id_ed25519
```

## Add the SSH key to your GitHub account

According to [📖 Github docs](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account), add the SSH key [here](https://github.com/settings/keys)

- Paste the content of the *public key*, `~/.ssh/id_ed25519.pub` to the key field.
- Add a descriptive label for the new key in the "Title" field.
- Finally, click the `Add SSH key` green button. If prompted, confirm your GitHub password.

## Add the SSH key to your GitLab account

Add the SSH key [here](https://gitlab.com/-/profile/keys)

- Paste the content of the *public key*, `~/.ssh/id_ed25519.pub` to the key field.
- Add a descriptive label for the new key in the "Title" field.
- Select an expiration date.
- Finally, click the `Add key` button.

## Test your setup

GitHub:

```sh
ssh -vT git@github.com
```

Accept its fingerprint if prompted. If you see "Hi <user>! You've successfully authenticated, but GitHub does not provide shell access)" that means voilà.

GitLab:

```sh
ssh -vT git@gitlab.com
```

Accept its fingerprint if prompted.

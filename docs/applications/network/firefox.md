---
title: Firefox Browser
tags:
  - web
  - linux
  - windows
---

Setup [Firefox browser](https://www.mozilla.org/firefox)

## Install

### Ubuntu

Install Firefox nightly from Mozilla's deb repo

```bash
# Create a directory to store APT repository keys if it doesn't exist:
sudo install -d -m 0755 /etc/apt/keyrings

# Import the Mozilla APT repository signing key:
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null

# The fingerprint should be 35BAA0B33E9EB396F59CA838C0BA5CE6DC6315A3
gpg -n -q --import --import-options import-show /etc/apt/keyrings/packages.mozilla.org.asc | awk '/pub/{getline; gsub(/^ +| +$/,""); print "\n"$0"\n"}'

# Next, add the Mozilla APT repository to your sources list:
echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null

# Update your package list and install the Firefox Nightly .deb package:
sudo apt-get update && sudo apt-get install -y firefox-nightly
```

### Windows

chocolatey:

```powershell
choco install firefox
```

winget:

```powershell
winget install -e --id Mozilla.Firefox
```

## Advanced settings

Enter `about:config` in the location bar

+ Set `browser.compactmode.show` to `true`

### Firefox Fullscreen Transition (Fade) & The Warning

From [this post](https://luis.adame.dev/blog/firefox-fullscreen-transition-timeout):

+ Set `full-screen-api.transition-duration.enter` to `0 0`
+ Set `full-screen-api.transition-duration.leave` to `0 0`
+ Set `full-screen-api.transition.timeout` to `0`
+ Set `full-screen-api.warning.timeout` to `0`

# Installation

My personal config files for a windows installation for WSL (ubuntu)

Assumes WSL already installed and running. If not: `wsl --install` from PowerShell admin.

## Git & SSH Setup

```bash
# Identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# SSH key
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub:    https://github.com/settings/keys
# Add to GitLab:    https://gitlab.com/-/profile/keys
# Authorize per-org on GitHub: https://github.com/settings/keys?q=type%3Assh

# GPG key
gpg --full-generate-key  # RSA 4096, no expiry recommended
gpg --armor --export you@example.com
# Add to GitHub: https://github.com/settings/keys
git config --global commit.gpgsign true
git config --global user.signingkey $(gpg --list-keys --keyid-format LONG you@example.com | grep -oP '(?<=rsa4096/)\w+')
```

## Base

```bash
sudo apt update && sudo apt upgrade
```

This file's `.bashrc` additions are **additive** — meant to sit on top of the default WSL bashrc, not replace it. Merge them in manually.

## Zoxide https://github.com/ajeetdsouza/zoxide

```bash
curl -sSfL https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | sh
```

## Oh-my-posh https://ohmyposh.dev/docs/installation/linux

```bash
curl -s https://ohmyposh.dev/install.sh | bash -s
```

Then install a Nerd Font (required for prompt glyphs): https://www.nerdfonts.com/font-downloads — download and extract a Nerd Font (JetBrainsMono Nerd Font recommended), then set it in your terminal (Ghostty or Windows Terminal settings). Restart terminal after setting font.

Or, use `oh-my-posh font install` to install the font for you (interactive)

## Nushell https://www.nushell.sh/book/installation.html

```bash
wget -qO- https://apt.fury.io/nushell/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/fury-nushell.gpg
echo "deb [signed-by=/etc/apt/keyrings/fury-nushell.gpg] https://apt.fury.io/nushell/ /" | sudo tee /etc/apt/sources.list.d/fury-nushell.list
sudo apt update
sudo apt install nushell
```

Switch to nu manually: run `nu` from bash. Auto-switching via `chsh` is skipped — zoxide eval in bashrc needs bash loaded first.

## Lazygit https://github.com/jesseduffield/lazygit#installation

For Debian 13 "Trixie", Sid, and later, or Ubuntu 25.10 "Questing Quokka" and later:

```bash
sudo apt install lazygit
```

For Debian 12 "Bookworm", Ubuntu 25.04 "Plucky Puffin" and earlier:

```bash
LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | \grep -Po '"tag_name": *"v\K[^"]*')
LAZYGIT_ARCH=$(uname -m | sed -e 's/aarch64/arm64/')
curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/download/v${LAZYGIT_VERSION}/lazygit_${LAZYGIT_VERSION}_Linux_${LAZYGIT_ARCH}.tar.gz"
tar xf lazygit.tar.gz lazygit
sudo install lazygit -D -t /usr/local/bin/

```

## Ghostty https://ghostty.org/docs/install/binary#ubuntu

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/mkasberg/ghostty-ubuntu/HEAD/install.sh)"
```

## Agent Harnesses

```bash
git clone git@github.com:Nirvaxstiel/AGENTS.git
```

Follow instructions to install and copy configs to relevant agents:

### Hermes-Agent https://hermes-agent.nousresearch.com/docs/getting-started/installation

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

Or via Podman/Docker. Check the AGENTS repo for more info.

## Opencode https://opencode.ai/docs/#installhttps://opencode.ai/docs/#install

Install via their bash script, or with NPM

```bash
curl -fsSL https://opencode.ai/install | bash
```

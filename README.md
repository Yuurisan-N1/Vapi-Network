<div align="center">

<img width="100%" alt="header" src="https://capsule-render.vercel.app/api?type=waving&height=210&text=Vapi%20Network%20Bot&fontAlign=50&fontAlignY=36&fontSize=56&desc=Auto%20Register%20%7C%20Identity%20Mint%20%7C%20Daily%20Claim%20%7C%20Multi-Account&descAlign=50&descAlignY=58"/>

<img alt="typing" src="https://readme-typing-svg.demolab.com?font=Inter&size=18&duration=3000&pause=650&center=true&vCenter=true&width=900&lines=Auto+Register+EVM+Wallets+%7C+SIWE+Auth;Turnstile+Verification+%7C+Auto+Solved;Identity+Mint+%7C+Username+%2B+Safety+Word+Auto-Generated;Auto+Daily+Quest+Claim+%7C+Points+Per+Cycle;All+Accounts+Saved+to+accounts.json"/>

<p>
  <img alt="ruby" src="https://img.shields.io/badge/Ruby-3.2+-CC342D?logo=ruby&logoColor=white"/>
  <img alt="platform" src="https://img.shields.io/badge/Platform-Vapi%20Network-111111"/>
  <img alt="proxy" src="https://img.shields.io/badge/Proxy-Supported-111111"/>
  <img alt="author" src="https://img.shields.io/badge/by-Yuurisandesu-111111"/>
</p>

<p>
  <b>Vapi Network Bot</b> is an account registration and daily reward automation tool for the Vapi Network platform.<br/>
  It creates fresh EVM wallets, signs them in via SIWE, mints an on-chain identity, picks a random username, stores a safety word, claims the daily quest reward, and saves every account to <code>accounts.json</code>, all looping automatically with proxy rotation and a live countdown between cycles.<br/>
  Built and distributed by <b>Yuurisandesu</b>.
</p>

</div>

<hr/>

<p align="center">
  <img src="image/image.png" alt="preview" width="100%"/>
</p>

<hr/>

---

## Table of Contents

- [Requirements](#requirements)
- [Install Ruby](#install-ruby)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Bot](#running-the-bot)
- [Features](#features)
- [File Structure](#file-structure)
- [Disclaimer](#disclaimer)

---

## Requirements

- Ruby `3.2+` (only needed to run the downloader script)

---

## Install Ruby

### Linux

```bash
sudo apt update && sudo apt install -y ruby git
```

### macOS

```bash
brew install ruby
```

### Windows

Download and run the installer from https://rubyinstaller.org. Check **Add Ruby executables to your PATH** during installation. Verify with:

```bash
ruby --version
```

### Termux (Android)

```bash
pkg update && pkg install ruby git
```

---

## Installation

**Clone the repository:**

```bash
git clone https://github.com/Yuurisan-N1/Vapi-Network.git
cd Vapi-Network
```

**Download the binary for your platform:**

```bash
ruby bot.rb
```

The script shows a numbered menu:

```
1. Vapi Linux ARM64
2. Vapi Linux AMD64
3. Vapi Windows x86_64
```

Enter the number for your platform. The binary downloads with a live progress bar and is set to executable automatically on Linux.

Or download manually from the Releases page:
https://github.com/Yuurisan-N1/Vapi-Network/releases/latest

| File | Platform |
|---|---|
| `vapi-linux-arm64` | Linux ARM64 |
| `vapi-linux-amd64` | Linux x86_64 |
| `vapi-windows-x86_64.exe` | Windows x86_64 |

**Linux after manual download:**

```bash
chmod +x vapi-linux-amd64
```

Place the binary in the same folder as `proxy.txt` and `config.json` before running.

---

## Configuration

### 1. Proxy (proxy.txt)

Fill `proxy.txt` with proxies, one per line (optional, leave empty to run without proxy):

```
host:port
host:port:user:pass
http://user:pass@host:port
```

Proxies are rotated across registration attempts in round-robin order. Proxy credentials are masked in log output.

### 2. Bot Settings (config.json)

`sleep_seconds` controls how many seconds the bot waits between full registration cycles. If `config.json` is missing, the bot falls back to a default of `3600` seconds.

---

## Running the Bot

**Linux / macOS / Android (Termux):**

```bash
./vapi-linux-amd64
```

**Linux ARM64:**

```bash
./vapi-linux-arm64
```

**Windows:**

```bash
.\vapi-windows-x86_64.exe
```

On first run, the bot asks two questions interactively:

1. **Enter the referral code** -- paste your referral code or a full referral URL. The code is extracted automatically from any format
2. **Enter the number of accounts** -- type how many accounts to register per cycle

After answering, the bot runs fully automatically. Press `Ctrl+C` at any time to stop cleanly.

---

## Features

### Auto Account Registration
The bot creates a fresh EVM wallet for each registration, sets the referral cookie, passes Turnstile verification automatically, and signs in using SIWE (Sign-In With Ethereum) on Base (chain ID 8453). No manual steps are needed after the initial prompts.

### Identity Mint
After sign-in, the bot picks a random username from a generated first name and last name combination. If a username is already taken, up to 6 alternatives are tried before the registration is skipped. Once a username is accepted, the bot mints the account identity on-chain and polls until the confirmation arrives. A two-word safety phrase is then generated and stored on the profile to complete the setup.

### Daily Quest Claim
After registration or sign-in to an existing account, the bot fetches the earn board, finds the daily quest, and claims it. The points awarded and the new total are logged. If the quest was already claimed that day, it is skipped with a note.

### Account Cache
Every registered account is saved to `accounts.json` with its wallet address, private key, username, safety word, referral code, and registration timestamp. On the next run, existing accounts in the cache are still counted toward the total. The file is updated after every successful registration.

### Referral Code Parsing
The referral code prompt accepts a bare code, a full URL, or a URL with query parameters. The code is extracted from any of these formats automatically.

### Proxy Rotation
Proxies from `proxy.txt` are assigned in round-robin order across registration attempts. Each attempt uses the next proxy in the list. Running without proxies is fully supported.

### Auto Countdown
After all registrations in a cycle are complete, the bot displays a live `HH:MM:SS` countdown until the next cycle starts.

### Graceful Shutdown
Pressing `Ctrl+C` prints `Script stopped by user` and exits cleanly.

---

## File Structure

```text
Vapi-Network/
├── vapi-linux-arm64            # Linux ARM64 binary
├── vapi-linux-amd64            # Linux x86_64 binary
├── vapi-windows-x86_64.exe     # Windows binary
├── bot.rb                      # Interactive downloader script (Ruby)
├── config.json                 # Sleep duration between cycles
├── proxy.txt                   # Proxy list, one per line (optional)
├── accounts.json               # Saved account records (auto-generated)
├── LICENSE                     # License file
├── image/                     
    └── image.png               # Preview script
└── utils/
    └── banner.rb               # Banner using yuurisan module
```

---

## Disclaimer

This tool is built for educational and technical exploration purposes. Use it wisely and at your own responsibility.

---

<div align="center">
<img width="100%" alt="footer" src="https://capsule-render.vercel.app/api?type=waving&height=120&section=footer"/>
</div>
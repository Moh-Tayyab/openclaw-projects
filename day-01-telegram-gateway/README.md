# 🚀 OpenClaw Multi-Channel AI Gateway (Telegram + WhatsApp)

> **New to this?** This project helps you set up your own AI Assistant on Telegram using a tool called OpenClaw. If you are in a region where Telegram is blocked, this guide shows you how to fix that and get the AI "brain" connected.

---

## 📖 Simple Glossary (For Beginners)
- **WSL2:** A way to run Linux (like Ubuntu) inside your Windows computer.
- **OpenClaw:** The software that acts as the "bridge" between your AI and Telegram.
- **ISP:** Your internet provider. Sometimes they block apps like Telegram.
- **Gateway:** A door that stays open to let messages flow between the AI and your phone.
- **API Key:** A secret password that gives your AI permission to use powerful "brains" (like Minimax or Gemini).

---

📋 Project Overview
The goal was to deploy a persistent AI Gateway capable of handling real-time tasks via Telegram. 

🎯 Key Objectives
- Deploy OpenClaw Gateway on Ubuntu (WSL2).
- Bypass regional internet blocks on Telegram.
- Connect a fast AI "brain" (Minimax-m2.7).
- Get the bot live and chatting!

🛠 The Journey: Challenges & Solutions

### 1. The Connection Blockade (The "Timeout" Era)
**The Problem:** The internet provider was blocking the connection to Telegram.
**The Fix:** 
1. We used **Cloudflare WARP** (like a VPN) to bypass the block.
2. We told the computer to use Google's address book (**DNS 8.8.8.8**) to find Telegram.

```bash
# This command tells your computer: "Use Google to find websites"
sudo sh -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
```

### 2. Authentication (The "Permission" Error)
**The Problem:** The AI said "Unauthorized."
**The Fix:** We provided a valid **API Key** (secret password) so the AI knew we were allowed to use it.

### 3. Gateway Synchronization (The "Busy" Error)
**The Problem:** Sometimes the software gets stuck in the background and won't start again.
**The Fix:** We "killed" the old stuck versions to make room for the new one.

```bash
# This command stops any old, stuck versions of OpenClaw
pkill -f openclaw
```

🏆 Achievements
- **Zero to Hero Time:** ~1.5 Hours (including network troubleshooting).
- **Model Integration:** Successfully connected Minimax-m2.7, providing sub-second response times.
- **Live Telegram Sync:** Fully paired with a Telegram bot account with a secure pairing/approval workflow.
- **Tooling:** Active plugins include Web Search, ACCPX Runtime, and Browser Control.

🚀 Deployment Guide (How to replicate)
1. **Install OpenClaw:** Follow the official shell script installation.
2. **Fix Network (if in restricted regions):**
   - Enable VPN/WARP on Host.
   - Update WSL DNS to `8.8.8.8`.
3. **Configure Model:**
   ```bash
   openclaw config
   # Select Provider -> Ollama/Cloud
   # Enter API Key for Minimax or Gemini
   ```
4. **Launch & Pair:**
   ```bash
   openclaw gateway
   # Approve in a new terminal:
   openclaw pairing approve telegram [CODE]
   ```

---

## 🟢 Phase 2: Multi-Channel Expansion (WhatsApp Integration)
After the Telegram bot was stable, we added WhatsApp **without turning off the system**. This shows that the OpenClaw Gateway can handle multiple apps at once without any "downtime" (switching off).

🎯 **Objectives**
- Add WhatsApp as a new way to talk to the AI.
- Keep the AI running on Telegram while setting up WhatsApp.
- Use the AI's own suggestions to guide the setup.

🛠 **The Process: Telegram to WhatsApp**
1. **Zero-Downtime Setup:** We kept the "Gateway" open on Telegram and used a second terminal window to set up WhatsApp. The AI never stopped working!
2. **AI-Guided Scaling:** The AI suggested using `wacli` (a tool for WhatsApp) and the same secure "Pairing Code" method we used for Telegram.
3. **Authentication:** 
   - We installed `wacli` to connect the computer to WhatsApp.
   - We scanned a QR code in the terminal to link the account.
   - We approved the connection using a simple command.

```bash
# This command connects your WhatsApp account to the AI
openclaw pairing approve whatsapp [CODE]
```

🏆 **Final Achievements (Day 1 - Part 2)**
- **Dual-Channel:** The AI now works on both Telegram and WhatsApp at the same time.
- **Scalable:** Proved we can add new channels (like WhatsApp) "on the fly" (while the system is running).
- **Tool Access:** WhatsApp users can now ask the AI to search the web or browse sites.

**New Tech Added:** `wacli`, WhatsApp Web Bridge.

---

📈 Final Result
The bot is now fully operational, responding to user queries on Telegram, and capable of performing web searches and executing shell tasks safely within the OpenClaw environment.

**Tech Stack:** Ubuntu (WSL2), OpenClaw, Ollama, Minimax-m2.7, Cloudflare WARP.

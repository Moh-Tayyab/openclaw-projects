# 🚀 OpenClaw AI Gateway: From Zero to Production-Ready

This repository documents the journey of setting up and deploying OpenClaw (v2026.4.21) on a Windows/WSL2 environment, overcoming ISP restrictions, and integrating a high-performance Cloud AI model for a live Telegram assistant.

📋 Project Overview
The goal was to deploy a persistent AI Gateway capable of handling real-time tasks via Telegram. The setup required bridging the gap between a local Linux environment (WSL2) and cloud-based LLM providers.

🎯 Key Objectives
- Deploy OpenClaw Gateway on Ubuntu (WSL2).
- Bypass regional ISP blocks on Telegram APIs.
- Configure a high-performance Cloud Model (Minimax-m2.7) for fast responses.
- Achieve a "Live" state for client demonstrations.

🛠 The Journey: Challenges & Solutions

### 1. The Connection Blockade (The "Timeout" Era)
**Problem:** Initial logs showed constant `UND_ERR_CONNECT_TIMEOUT`. This was due to ISP restrictions in Pakistan blocking Telegram's API endpoints.

**Solution:** 
* Implemented Cloudflare WARP on the host Windows machine.
* Forced Ubuntu (WSL2) to use Google DNS by overriding `/etc/resolv.conf`:

```bash
sudo sh -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
```
* Verified connectivity using `curl -4 -v https://api.telegram.org`.

### 2. Authentication Hurdles (HTTP 401)
**Problem:** While the network was fixed, the AI model returned "Unauthorized" errors because the Cloud Model (Kimi/Minimax) required a valid API Key.

**Solution:**
* Switched to `Minimax-m2.7:cloud` via Ollama launch.
* Configured the environment to handle secure API authentication.

### 3. Gateway Synchronization
**Problem:** Port conflicts (18789) when multiple gateway instances tried to start.

**Solution:** 
* Used `pkill -f openclaw` to clear zombie processes.
* Executed a clean launch using:

```bash
ollama launch openclaw --model minimax-m2.7:cloud
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

📈 Final Result
The bot is now fully operational, responding to user queries on Telegram, and capable of performing web searches and executing shell tasks safely within the OpenClaw environment.

**Tech Stack:** Ubuntu (WSL2), OpenClaw, Ollama, Minimax-m2.7, Cloudflare WARP.

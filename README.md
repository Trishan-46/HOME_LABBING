# HOME_LABBING
# 🔐 Connecting Kali Linux to TryHackMe
 
A step-by-step guide to connecting your Kali Linux machine to TryHackMe using OpenVPN.
 
---
 
## Prerequisites
 
- Kali Linux (VM or bare metal)
- A free account at [tryhackme.com](https://tryhackme.com)
- Internet connection
---
 
## Step 1 — Download the VPN Configuration File
 
1. Log in to [tryhackme.com](https://tryhackme.com).
2. Click your profile icon → **Access**.
3. Under **VPN Access**, select your server region (e.g., EU-Regular-1).
4. Click **Download My Configuration File** — saves a `.ovpn` file.
---
 
## Step 2 — Install OpenVPN on Kali
 
OpenVPN comes pre-installed on Kali. If it's missing:
 
```bash
sudo apt update && sudo apt install -y openvpn
```
 
---
 
## Step 3 — Connect to the VPN
 
```bash
sudo openvpn --config ~/Downloads/your-username.ovpn
```
 
> Keep this terminal open — closing it will disconnect the VPN.
 
You'll know it's connected when you see:
 
```
Initialization Sequence Completed
```
 
---
 
## Step 4 — Verify the Connection
 
Open a new terminal and check for the `tun0` interface:
 
```bash
ip addr show tun0
```
 
You should see a `10.x.x.x` IP address — that's your TryHackMe VPN IP.
 
---
 
## Step 5 — Start Hacking a Room
 
1. On TryHackMe, open any room and click **Start Machine**.
2. Wait ~1 minute for the target machine to boot — you'll get a target IP.
3. Test reachability from Kali:
```bash
ping <target-ip>
```
 
4. Start enumeration:
```bash
nmap -sV <target-ip>
```
 
---
 
## Troubleshooting
 
| Problem | Fix |
|---|---|
| `tun0` not found | Re-download the `.ovpn` file from your Access page |
| "AUTH_FAILED" error | Regenerate the config file on TryHackMe |
| Can't reach target IP | Confirm VPN is active (`ip addr show tun0`) |
| Already connected error | Only one active VPN session per account — disconnect first |
 
---
 
## Notes
 
- Always run OpenVPN with `sudo` — it needs root to create the tunnel interface.
- The VPN disconnects if your terminal or machine sleeps — just reconnect with the same command.
- TryHackMe allows only **one active VPN connection** per account at a time.
---
 
> ⚠️ **Legal Notice**: Only attack machines on TryHackMe that you have started yourself. Never use these techniques on systems you don't own or have permission to test.
 

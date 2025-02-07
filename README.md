# Advanced NTP & NTPQ Cheat Sheet

## 🔹 Basic Commands

| Command | Description |
|---------|-------------|
| `ntpq -p` | Show NTP peers (status of connected servers) |
| `ntpq -c peers` | Same as `ntpq -p` (displays list of peers) |
| `ntpq -c assoc` | Show association IDs for connected servers |
| `ntpq -c rv` | Show system variables (runtime variables) |
| `ntpq -c version` | Display `ntpq` version |
| `ntpq -c "rv 0"` | Show synchronization status and system variables |
| `ntpq -p <server>` | Query a specific NTP server |

## 🔹 Interactive Mode  
Run `ntpq` without arguments to enter interactive mode. Then use:

| Command | Description |
|---------|-------------|
| `peers` | Show NTP peers with basic status |
| `assoc` | Show association IDs |
| `rv` | Display system variables |
| `lpeers` | Show detailed peer list (like `peers`, but includes delay, jitter, etc.) |
| `mreadlist` | Read multiple variables from all peers |

## 🔹 Peer Status Flags (`ntpq -p` or `peers`)

| Symbol | Meaning |
|--------|---------|
| `*` | System peer (currently synced) |
| `#` | Backup peer (not used, but good candidate) |
| `+` | Candidate peer (could be used for sync) |
| `-` | Disqualified peer (not used for sync) |
| `x` | Falseticker (unreliable time source) |
| `o` | PPS peer (high-precision time source) |

## 🔹 Common NTP Configuration Files

| File | Description |
|------|-------------|
| `/etc/ntp.conf` | Main NTP configuration file |
| `/var/lib/ntp/ntp.drift` | Stores frequency error (drift) data |
| `/etc/ntp/step-tickers` | List of NTP servers used at startup |

## 🔹 Checking Synchronization Status

| Command | Description |
|---------|-------------|
| `ntpq -c "rv 0"` | Display system variables (offset, stratum, root delay, reftime, etc.) |
| `ntpq -c "lassoc"` | List all known associations |
| `ntpstat` | Quick synchronization status summary |

## 🔹 Querying a Specific NTP Server

| Command | Description |
|---------|-------------|
| `ntpq -p <server>` | Query the given NTP server for peer information |
| `ntpq -c "rv <assoc_id>"` | Get details about a specific association |

## 🔹 Forcing NTP Sync

| Command | Description |
|---------|-------------|
| `sudo systemctl restart ntp` | Restart NTP service |
| `sudo ntpdate -u pool.ntp.org` | Manually sync time with an NTP server |
| `timedatectl set-ntp true` | Enable NTP synchronization using `systemd` |
| `sudo hwclock --systohc` | Sync hardware clock with system time |

## 🔹 Debugging NTP Issues

| Issue | Command | Possible Fix |
|-------|---------|--------------|
| NTP service not running | `systemctl status ntp` | Start it: `sudo systemctl start ntp` |
| Clock is out of sync | `ntpq -p` | Run `sudo ntpdate -u pool.ntp.org` |
| NTP servers not reachable | `ntpq -c peers` | Check firewall rules (UDP port 123) |
| NTP drift file issues | `cat /var/lib/ntp/ntp.drift` | Delete drift file and restart NTP |

## 🔹 Useful NTP Servers

| Server | Provider |
|--------|----------|
| `pool.ntp.org` | Public NTP Pool Project |
| `time.google.com` | Google NTP |
| `time.windows.com` | Microsoft NTP |
| `time.apple.com` | Apple NTP |
| `ntp.ubuntu.com` | Ubuntu NTP |

---

🔥 **Now you're equipped with advanced NTP & NTPQ commands for troubleshooting and managing time synchronization!** 🚀

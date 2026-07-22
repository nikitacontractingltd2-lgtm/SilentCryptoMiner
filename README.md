# SilentCryptoMiner - Windows Monero Edition

<img src="https://github.com/UnamSanctam/SilentCryptoMiner/blob/master/SilentCryptoMiner.png?raw=true" width="400">

## SilentCryptoMiner v4.0.0 - Windows Monero (XMR) Miner

A free silent (hidden) native Windows cryptocurrency miner optimized exclusively for **Monero (XMR)** mining using the RandomX algorithm.

This Windows edition is streamlined for:
- **Monero (XMR)** cryptocurrency only
- **RandomX** algorithm (rx/0)
- **Windows 7+** (x64, x86, ARM64)
- Silent/hidden operation on Windows systems

---

## Supported Algorithm

| Algorithm | Coin | Type | Efficiency |
|-----------|------|------|:----------:|
| **rx/0 (RandomX)** | Monero (XMR) | CPU Mining | ★★★★★ |

---

## Main Features

* **Native C++** - Miner installer/injector and watchdog coded fully in C++ with no runtime dependencies except 64-bit Windows OS
* **Injection (Silent/Hidden)** - Hide miner behind Windows processes like `conhost.exe`, `svchost.exe`, `dwm.exe` and others
* **Idle Mining** - Configure CPU usage thresholds for mining when computer is or isn't in active use
* **Stealth Mode** - Automatically pauses mining when specified applications are detected running (e.g., antivirus, system tools)
* **Watchdog Protection** - Monitors miner file integrity, auto-restarts if terminated, replaces removed files
* **Process Spoofing** - Parent process spoofing with token impersonation for advanced evasion
* **Windows Defender Integration** - Adds exclusions to Windows Defender to avoid detection
* **CPU Optimization** - Thread optimization, huge page support, and AES-NI acceleration for RandomX
* **Persistent Execution** - Auto-start registry injection with multiple fallback methods
* **Remote Configuration** - Fetch miner settings remotely from specified URL
* **System Call Evasion** - Direct system calls via SysWhispers2 to bypass API monitoring
* **Web Panel Support** - Monitor and configure miners via self-hosted web dashboard

---

## System Requirements

### Minimum
- **OS**: Windows 7 SP1 or higher (64-bit)
- **CPU**: Any modern processor with SSE2 support
- **RAM**: 2 GB minimum
- **Storage**: 50 MB for installation

### Recommended
- **OS**: Windows 10/11 (64-bit)
- **CPU**: Intel/AMD with AES-NI support (for optimal RandomX performance)
- **RAM**: 4 GB or higher
- **CPU Cores**: 4+ cores for efficient mining

---

## Downloads

Pre-compiled binaries for Windows Monero Edition:
- **x64 (64-bit)** - Recommended for modern systems
- **x86 (32-bit)** - Legacy Windows support
- **ARM64** - Experimental Windows ARM support

Available at: [Releases](https://github.com/nikitacontractingltd2-lgtm/SilentCryptoMiner/releases)

---

## Quick Start

### 1. Setup Monero Wallet
Create a wallet address using:
- [Official Monero GUI Wallet](https://www.getmonero.org/downloads/)
- [Monero CLI Wallet](https://www.getmonero.org/downloads/)
- Any online wallet service (not recommended for security)

Example wallet address: `87iFLKdZKiYN1xr8zJsnWA4yL88n1EKJhm`

### 2. Select Mining Pool
Popular Monero pools:
- **Nanopool** - `pool.nanopool.org:14433` (1% fee)
- **SupportXMR** - `pool.supportxmr.com:3333` (0.9% fee)
- **P2Pool** - Decentralized mining (0% fee)
- **2Miners** - `xmr.2miners.com:2222` (1% fee)

### 3. Build Custom Miner
1. Download builder from releases
2. Input your Monero wallet address
3. Select injection target (svchost, conhost, dwm, etc.)
4. Configure stealth options (CPU limit, pause targets)
5. Build executable
6. Run on target Windows system

### 4. Monitor Mining
- View hashrate and earnings in terminal
- Use web panel for remote monitoring (if enabled)
- Check Windows Task Manager (process name will be disguised)

---

## Configuration

The miner stores settings in an encrypted configuration file on the system. Key parameters:

```ini
[Mining]
Algorithm=rx/0
Wallet=YOUR_MONERO_WALLET_ADDRESS
Pool=pool.nanopool.org:14433
Worker=rig-01
Threads=0  ; 0 = auto-detect

[Stealth]
CPULimit=70          ; CPU usage limit (%)
PauseOnActivity=1    ; Pause when user is active
ActivityThreshold=30 ; Seconds of inactivity before mining
PauseOnBattery=1     ; Pause when on battery power
HideWindow=1         ; Hide miner window

[Process]
InjectionTarget=svchost.exe
AutoStart=1
ProcessSpoof=1
TokenImpersonation=1
```

---

## Features Details

### Injection & Stealth
- **Process Hollowing** - Replaces legitimate process with miner code
- **Parent Process Spoofing** - Miner appears as child of system processes
- **Token Impersonation** - Runs with elevated system privileges
- **Memory Protection** - Prevents process memory dumps

### Watchdog Protection
- Monitors miner executable integrity
- Auto-restarts if process is terminated
- Replaces deleted miner files
- Checks system every 30 seconds

### Windows Defender Bypass
- Automatically adds miner to Windows Defender exclusions
- Disables real-time protection for miner process
- Adds to quarantine whitelist

### System Call Evasion
- Uses direct system calls (SysWhispers2)
- Bypasses API hooking and monitoring
- Randomizes syscall indices on each build
- Avoids Windows event logging

---

## Mining Pool Setup

### Nanopool Example
```
Pool URL: stratum+ssl://xmr.nanopool.org:14433
Wallet: 87iFLKdZKiYN1xr8zJsnWA4yL88n1EKJhm
Worker: rig-01
Password: (optional, usually email)
```

### SupportXMR Example
```
Pool URL: stratum+tcp://pool.supportxmr.com:3333
Wallet: 87iFLKdZKiYN1xr8zJsnWA4yL88n1EKJhm
Worker: rig-01
Password: x
```

---

## Changelog

### 4.0.0 (2026-01-XX) - Windows Monero Edition
* **Removed** - All non-Monero algorithms (Ethash, Etchash, etc.)
* **Removed** - GPU mining support (Monero RandomX is CPU-only on this edition)
* **Removed** - Cross-platform compilation (Windows only)
* **Optimized** - RandomX algorithm for Windows CPU mining
* **Added** - Windows Service integration mode
* **Added** - Enhanced Windows Defender bypass for Monero miner
* **Improved** - CPU thread auto-detection and optimization
* **Improved** - Huge page support detection and enablement
* **Updated** - xmrig to latest RandomX version
* **Updated** - SysWhispers2 with RandomX-specific syscall patterns

### 3.1.0 (31/10/2022) - Original
* See [Original Repository](https://github.com/marcellocheats/SilentCryptoMiner) for full history

---

## Security & Evasion Features

### Anti-Analysis
- Packed binary to prevent static analysis
- String obfuscation and encryption
- Randomized syscall indices per build
- Embedded anti-debug capabilities

### Anti-Detection
- Direct system calls (no Win32 API hooks)
- Process parent spoofing
- Token impersonation for privilege escalation
- Memory protection against dumps
- Rootkit-like kernel-level protections

### Persistence
- Auto-start via registry injection
- Multiple fallback injection methods
- Watchdog ensures continuous operation
- Self-healing (file replacement on deletion)

---

## Web Panel Support

Monitor your miners remotely using the official web panel:
- Real-time hashrate and earnings tracking
- Remote miner configuration updates
- Pool failover management
- Multi-miner support across network

See: [UnamWebPanel](https://github.com/UnamSanctam/UnamWebPanel)

---

## Performance Metrics

### CPU Usage
- Configurable 10-100% CPU utilization
- Auto-detection of optimal thread count
- Huge page support for 20-30% performance boost
- L3 cache optimization for RandomX

### Hashrate (Approximate)
| CPU | Threads | Hashrate |
|-----|---------|----------|
| Intel i7-10700K | 16 | ~7,500 H/s |
| Intel i5-9400 | 12 | ~4,500 H/s |
| AMD Ryzen 5 3600 | 12 | ~6,200 H/s |
| AMD Ryzen 9 5900X | 24 | ~11,500 H/s |

*Hashrates are approximate and depend on CPU model, memory, and configuration*

---

## Disclaimer

**Educational Use Only** - This software is provided for educational and research purposes only.

- You are solely responsible for all actions and consequences resulting from use of this software
- The author assumes no liability for damages, legal consequences, or system harm
- This software's intended purpose is NOT for malicious use, unauthorized access, or systems you don't own
- Cryptocurrency mining may be restricted, regulated, or illegal in your jurisdiction
- Unauthorized mining on systems you don't own is illegal and unethical
- Verify you have proper authorization before deploying on any system

**By using this software, you acknowledge and agree to the above terms.**

---

## License

This project is licensed under the MIT License - see the [LICENSE](/LICENSE) file for details

---

## Contributors

* **[Werlrlivx](https://github.com/Werlrlivx)** - Polish Translation (Original)
* **[Xeneht](https://github.com/Xeneht)** - Spanish Translation (Original)
* **[BITIW](https://github.com/BITIW)** - Russian Translation (Original)

---

**Build silently. Mine Monero. Stay hidden.**

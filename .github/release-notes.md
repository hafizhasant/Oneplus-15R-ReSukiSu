## 🔧 Kernel Build for OnePlus 15 / 15R

**Kernel:** 6.12.58-android16-5
**KSU:** ReSukiSU
**SUSFS:** v2.3.0

### ✨ Enabled in this build
- ReSukiSU root
- SUSFS v2.3.0
- Boeffla wakelock blocker
- ADIOS block MQ I/O scheduler (default)
- BBRv3 congestion control
- Netfilter + IPSet
- IPv6 NAT
- Sultan-derived power/memory tweaks
- GKID misc patches:
  - F2FS GC urgent sleep → 50 ms
  - F2FS `min_fsync_blocks` → 20
  - Freezer timeout → 1 s
  - ext4 commit age increased
  - ARM64 mem-op optimizations
  - `lib/string.c` optimizations
  - Alarmtimer wake minimization
  - IRQ + printk log silence
- MGLRU compiled in

### 🧩 Runtime tuning (apply after flash)
See README for the boot scripts that enable:
- MGLRU + `min_ttl_ms=2000`
- GPU power level cap (891 MHz)
- Wakelock blocklist
- TCP `bbr3`

### 📦 Installation
1. Download the ZIP below
2. Reboot to recovery / KernelSU Manager
3. Flash the ZIP
4. Reboot

### ⚠️ Notes
- Keep a backup boot image before flashing
- fastboot/recovery access recommended in case of issues

### 🙏 Credits
All kernel code belongs to its upstream authors — Google AOSP, ReSukiSU, SUSFS (simonpunk), Boeffla (andip71), GKID-Kernels (ahmed-alnassif), WildKernels, AnyKernel3 (osm0sis), and the BBRv3 / ADIOS maintainers. See README for the full list.

# 🚀 OnePlus 15 / 15R ReSukiSU Kernel Builder

GitHub Actions workflow for building flashable **ReSukiSU GKI kernels** for the **OnePlus 15** and **OnePlus 15R**.

It syncs Android GKI sources, adds **ReSukiSU**, optionally applies **SUSFS**, and packages the result as an **AnyKernel3 ZIP**.

---

## 📱 Supported Devices

| Device | ID | Codename | SoC | GKI Branch |
|---|---|---|---|---|
| OnePlus 15 | `oneplus15` | `Infinity` | `sm8850` | `android16-6.12-2025-06` |
| OnePlus 15R | `oneplus15r` | `macan` | `sm8845` | `android16-6.12-2025-12` |

> This builder produces a **generic GKI** `kernel_aarch64` Image, so the device only selects the GKI branch and the ZIP name. `DEVICE=all` compiles both branches — one Image for `sm8850`, one for `sm8845`.

---

## ✨ Features

### Core
- ReSukiSU integration
- Optional SUSFS
- Optional Sultan-derived power/memory tweaks (WildKernels patches, dry-run checked)
- Optional Unicode invisible-codepoint bypass patch
- Flashable AnyKernel3 ZIP
- GitHub Release or artifact output

### Networking
- Optional Netfilter + IPSet
- Optional BBR + ECN
- Optional BBRv3 backport (KMI-safe on `android16-6.12`)
- Net schedulers built in: `fq`, `fq_codel`, `cake`
- IPv6 NAT fix

### Scheduler & I/O
- Optional ADIOS block MQ I/O scheduler (default)

### Memory
- MGLRU compiled in (`CONFIG_LRU_GEN=y` / `CONFIG_LRU_GEN_ENABLED=y`)

### Battery & Thermal
- Optional Boeffla wakelock blocker — **with 6.12 build fix included**

### GKID misc patches (optional, toggleable)
- F2FS GC urgent sleep reduced to 50 ms
- F2FS `min_fsync_blocks` enlarged to 20
- Freezer timeout reduced to 1 s
- ext4 default commit age increased
- ARM64 memory-op optimizations (memcpy / memset / memcmp)
- `lib/string.c` optimized mem operations
- Alarmtimer wake minimization
- IRQ log spam silence
- printk spam silence

> ⚠️ **LSM / Baseband Guard is not listed** — it does not work on 6.12 kernels.

---

## 🚀 Quick Start

1. Fork this repo
2. Open **Actions**
3. Run the workflow
4. Select your device and options
5. Download the generated ZIP
6. Flash via KernelSU / Magisk / recovery

---

## ⚙️ Key Options

| Option | Description |
|---|---|
| `DEVICE` | `oneplus15`, `oneplus15r`, or `all` |
| `KSU_META` | ReSukiSU source: `branch/tag/commit` |
| `SUSFS_META` | Empty = latest, `-1` = disabled, hash = pinned |
| `NETFILTER` | Enable Netfilter/IPSet |
| `BBR_ECN` | Enable BBR + ECN |
| `BBR3` | Backport BBRv3 (patches `net/tcp`, adds `CONFIG_TCP_CONG_BBR3`) |
| `ADIOS` | Add the ADIOS block MQ I/O scheduler and make it the default |
| `BOEFFLA_WL_BLOCKER` | Boeffla wakelock blocker — 6.12 build fix applied automatically |
| `SULTAN_TWEAKS` | Sultan-derived power/memory tweaks |
| `GKID_PATCHES` | GKID misc patches (F2FS GC, freezer timeout, mem-op, ext4 commit, log silence) |
| `CREATE_RELEASE` | Publish ZIP to GitHub Releases |

---

---

## 📦 Output

Naming: `AK3_ReSukiSU_<ksuver>_<SUSFS-ver|noSUSFS>_<device>_<kernel>.zip`

Examples:
- `AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15_6.12.0.zip`
- `AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15R_6.12.0.zip`
- `AK3_ReSukiSU_43000_noSUSFS_OnePlus15_6.12.0.zip`

---

## ⚠️ Notice

Use at your own risk. Keep a backup boot image and make sure fastboot/recovery access is available.

---

## 🙏 Credits

This project is a build orchestration layer. The actual kernel code comes from the following upstreams — **all credit goes to their maintainers**:

- **Google / AOSP** — Android GKI kernel (`android16-6.12`)
- **ReSukiSU** — KernelSU fork used as the root solution
- **SUSFS (simonpunk)** — Kernel-based root-hiding filesystem patches
- **Boeffla (andip71)** — Wakelock blocker driver
- **GKID-Kernels (ahmed-alnassif)** — Misc kernel patches (F2FS, freezer, mem-op, log silence)
- **WildKernels** — Sultan-derived tweaks
- **Numbersf** — Reference for GKI build workflows and scheduler patches
- **AnyKernel3 (osm0sis)** — Flashable zip template
- **BBRv3** — Congestion control backport
- **ADIOS** — Block MQ I/O scheduler

If you authored any of the patches included here and would like attribution changed, open an issue or PR.

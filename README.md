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

- ReSukiSU integration
- Optional SUSFS
- Optional Netfilter + IPSet
- Optional BBR + ECN
- Optional BBRv3 backport (KMI-safe on android16-6.12)
- Net schedulers built in: `fq`, `fq_codel`, `cake`
- Optional ADIOS block MQ I/O scheduler
- Optional Sultan kernel tweaks
- Optional Boeffla wakelock blocker — **with 6.12 build fix included** (see below)
- Optional Unicode bypass patch
- MGLRU compiled in (`CONFIG_LRU_GEN=y` / `CONFIG_LRU_GEN_ENABLED=y`)
- Flashable AnyKernel3 ZIP
- GitHub Release or artifact output
- Build logs, hashes, and summary

> ⚠️ **LSM / Baseband Guard is not listed** — it does not work on 6.12 kernels.

---

## 🚀 Quick Start

1. Fork this repo
2. Open **Actions**
3. Run the workflow
4. Select your device and options
5. Download the generated ZIP

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
| `SULTAN` | Apply Sultan-derived kernel tweaks |
| `BOEFFLA_WL_BLOCKER` | Boeffla wakelock blocker — 6.12 build fix applied automatically |
| `CREATE_RELEASE` | Publish ZIP to GitHub Releases |

---

## 📦 Output

Naming: `AK3_ReSukiSU_<ksuver>_<SUSFS-ver|noSUSFS>_<device>_<kernel>.zip`

Examples:
- `AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15_6.12.0.zip`
- `AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15R_6.12.0.zip`
- `AK3_ReSukiSU_43000_noSUSFS_OnePlus15_6.12.0.zip`

> Building `DEVICE=all` compiles both unique kernels — one for `sm8850` (OnePlus 15) and one for `sm8845` (OnePlus 15R) — producing two ZIPs.

---

## ⚠️ Notice

Use at your own risk. Keep a backup boot image and make sure fastboot/recovery access is available.

---

## 🙏 Credits

Thanks to the maintainers of Android GKI, ReSukiSU, SUSFS, AnyKernel3, Boeffla wakelock blocker, Sultan kernel tweaks, and related community patches.

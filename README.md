# -EvolutionX-custom-ROM-MI-A3

# ✅ Successfully Installed EvolutionX on Mi A3 (laurel_sprout)

This repository documents how I installed the [EvolutionX 15.0](https://evolution-x.org/) custom ROM on my **Mi A3** (code name: `laurel_sprout`), overcoming soft brick issues, A/B slot confusion, and sideload failures.

---

## 📱 Device Info

- **Device:** Xiaomi Mi A3
- **Codename:** laurel_sprout
- **ROM Installed:** [EvolutionX 15.0 - 20250510 Official](https://evolution-x.org/)
- **Recovery Used:** LineageOS Recovery (alternatively, TWRP works too)
- **Bootloader:** Unlocked

---

## 🔧 Prerequisites

- ADB & Fastboot installed on your PC
- Unlocked bootloader
- USB cable (preferably USB 2.0, avoid USB hubs)
- Basic knowledge of flashing via terminal

---

## 📦 Required Files

Place all these in one folder:
- `boot.img`
- `vbmeta.img`
- `dtbo.img`
- `EvolutionX-15.0-20250510-laurel_sprout-10.6-Official.zip`
- (Optional: `stock` or `custom recovery` like `lineage-recovery.img`)

---

## ⚙️ Flashing Steps

### 1. Boot into Fastboot Mode

```bash
adb reboot bootloader
````

### 2. Flash Critical Partitions to Slot B

```bash
fastboot flash boot_b boot.img
fastboot flash vbmeta_b vbmeta.img
fastboot flash dtbo_b dtbo.img
```

> You can also flash to both slots if needed:
> `fastboot flash boot_a boot.img` and so on.

### 3. Set Active Slot to B

```bash
fastboot set_active b
```

### 4. Boot to Recovery

```bash
fastboot reboot recovery
```

---

## 📥 Install the ROM via ADB Sideload

In recovery:

* Select: **Apply Update > ADB Sideload**

Then run:

```bash
adb sideload EvolutionX-15.0-20250510-laurel_sprout-10.6-Official.zip
```

> ⚠️ If stuck at 47%, reboot recovery and use `adb push` instead.

---

## 🧼 Format Data (Important)

After sideloading:

* In recovery: **Factory Reset** or **Format Data**

---

## 🚀 Reboot to System

```bash
adb reboot
```

---

## 🧯 In Case of Soft-Brick or EDL Mode

If the phone gets stuck in **Qualcomm QDL Mode (EDL)**:

```bash
lsusb
# Output should show: Qualcomm, Inc. Gobi Wireless Modem (QDL mode)
```

Flash stock ROM via:

* 🪟 **Windows:** Mi Flash Tool
* 🐧 **Linux:** [`edl`](https://github.com/bkerler/edl) tool (advanced)

---

## 🔁 Troubles I Faced

* `adb sideload` getting stuck at 47%
* A/B slot mismatch (bootloop on slot A)
* Device soft-bricked into EDL mode (QDL 9008)
* Solved by flashing everything to slot B and setting it active

---

## 🙌 Final Result

* Booted successfully into **EvolutionX 15.0**
* System is smooth, stable, and rooted (optional)
* Verified via `fastboot getvar current-slot`

---

## 🔗 Helpful Links

* [LineageOS Wiki for Mi A3](https://wiki.lineageos.org/devices/laurel_sprout/install/)
* [Xiaomi Firmware Updater](https://xiaomifirmwareupdater.com/)
* [bkerler/edl tool](https://github.com/bkerler/edl)
* [EvolutionX Website](https://evolution-x.org/)


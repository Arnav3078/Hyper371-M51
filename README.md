# Hyper371-M51

Experimental **HyperOS 3.1 / Hyper371 port for the Samsung Galaxy M51 (SM-M515F)**.

> **Development status: v0.1 TEST**
>
> Extensive static verification has been completed, but the first confirmed public boot is still pending. This is not a stable ROM.

## Project Goal

Bring the Hyper371 HyperOS userspace to the Galaxy M51 while retaining the Galaxy M51 hardware stack required for actual device compatibility.

This is **not a generic GSI**.

## Target

- Device: Samsung Galaxy M51
- Model: `SM-M515F`
- Platform: Qualcomm SM7150 family
- Test firmware baseline: `M515FXXS6DXE3`
- Rollback protection: `RP6`
- Hardware identity check used by the test installer: `ro.boot.em.model=SM-M515F`

## Architecture

| Component | Source |
|---|---|
| `system` | Hyper371 |
| embedded `system_ext` | Hyper371 |
| `product` | Hyper371 |
| `vendor` | Galaxy M51 |
| `odm` | Galaxy M51 |
| `boot` / kernel | Galaxy M51 |
| `dtbo` | Galaxy M51 |
| modem / radio firmware | Existing M51 firmware |

Filesystem layout:

    /
    ├── system/
    │   ├── system_ext/       <- Hyper371 system_ext
    │   └── product -> /product
    ├── system_ext -> /system/system_ext
    ├── product/              <- Hyper371 product
    ├── vendor/               <- M51 vendor
    └── odm/                  <- M51 ODM

The port keeps M51 hardware-specific camera, fingerprint, RIL/IMS, Wi-Fi/Bluetooth, sensors, audio, charging/thermal, init and SELinux hardware policy components wherever possible while preserving Hyper371 userspace/features.

## Current Progress

Completed:

- Hyper371 donor ROM extracted and analyzed
- Known-good M51 reference ROM analyzed
- Dynamic partition layout reconstructed
- Hyper371 system layout converted for M51
- Hyper371 `system_ext` embedded into `/system/system_ext`
- Hyper371 `product` moved to the real M51 `product` partition
- M51 `vendor` and `odm` retained
- M51 `boot.img` and `dtbo.img` retained
- EROFS `system.img` and `product.img` generated
- EROFS integrity checks passed
- SELinux xattrs verified after EROFS creation
- Hyper371 + M51 SELinux policy compile test passed
- M51 FCM level-5 HAL compatibility precheck passed
- Dynamic partition capacity check passed with ~3.27 GiB free
- Experimental test vbmeta generated
- Recovery payload and installer generated
- Final ZIP integrity test passed
- M51 boot ramdisk / first-stage fstab verified
- Physical device firmware baseline verified
- Download Mode and OEM unlock state verified
- EFS and `sec_efs` backups verified before testing

Pending:

- To Actually Test The ROM

## Dynamic Partitions

M51 dynamic group maximum:

    8,048,869,376 bytes

Current v0.1 allocation:

    system   1,435,795,456
    product  2,287,689,728
    vendor     809,484,288
    odm            606,208
    -----------------------
    total    4,533,575,680
    free     3,515,293,696

Approximately **3.27 GiB remains free**.

See [docs/PARTITIONS.md](docs/PARTITIONS.md).

## SELinux

The M51 vendor declares `plat_sepolicy_vers = 30.0`. Hyper371 contains the required Android `30.0` compatibility mapping.

Offline combined policy compilation result:

    secilc return code: 0
    SELINUX COMPILE: PASS

Permissive SELinux is not intended as a final solution.

See [docs/SELINUX.md](docs/SELINUX.md).

## VINTF

The M51 vendor manifest reports `target-level="5"`.

The Hyper371 framework includes FCM matrices for levels `5`, `6`, `7`, `8`, and `202404`.

Development HAL compatibility precheck:

    Mandatory FAIL      : 0
    Mandatory UNCHECKED : 0

This is not a replacement for official Android `checkvintf` / VTS testing.

See [docs/VINTF.md](docs/VINTF.md).

## AVB

The original Samsung vbmeta descriptors cannot validate modified Hyper371 partitions.

The current v0.1 development build uses:

    Algorithm: NONE
    Flags: 3

This disables AVB verification and dm-verity for the experimental test build only. It is not intended as the final release security configuration.

See [docs/AVB.md](docs/AVB.md).

## v0.1 Test Build

Filename:

    Hyper371_M51_v0.1_TEST.zip

SHA-256:

    afdc447ca4453d4848a748da571229e3995213cef1ec4f9232053e67340b3a86

The ROM ZIP itself is not stored in this repository.

## Safety

Before testing:

- use **SM-M515F only**
- have an unlocked bootloader
- use compatible `M515FXXS6DXE3` / `RP6` firmware
- have working recovery and Download Mode
- back up personal data
- make verified EFS / `sec_efs` backups
- keep known-good M51 Odin firmware available

The v0.1 installer intentionally does **not** flash A71 firmware, modem/radio firmware, or Samsung bootloader firmware.

## Proprietary Files

This repository intentionally does not include proprietary Samsung/Xiaomi firmware, complete ROM images, device-private EFS data, third-party recovery binaries, or the complete flashable ROM package.

Users must obtain proprietary files legally themselves.

## Project Status

**v0.1 — First Boot Testing**

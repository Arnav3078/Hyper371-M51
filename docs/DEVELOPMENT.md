# Development History

## 1. Donor analysis

Hyper371 was identified as a full Android 15 / HyperOS port rather than a generic GSI.

The donor Galaxy A71 and target Galaxy M51 both use Qualcomm SM6150-era Samsung vendor stacks, making the A71 a useful compatibility reference.

## 2. Target reference analysis

A known-working Galaxy M51 custom ROM was used only as a target hardware/layout reference.

The current M51 dynamic layout uses:

    system
    vendor
    product
    odm

## 3. Filesystem conversion

The port was converted to the M51 partition model:

    system.img
      Hyper371 /system
      Hyper371 system_ext -> /system/system_ext

    product.img
      Hyper371 /product

    vendor.img
      Galaxy M51

    odm.img
      Galaxy M51

## 4. SELinux relabeling

Moving product and system_ext content required restoring the Hyper371 SELinux labels before image generation.

Representative labels were verified before and after EROFS creation.

## 5. EROFS generation

New `system.img` and `product.img` images were generated as EROFS and passed filesystem integrity verification.

## 6. SELinux compatibility

Hyper371 platform policy compiled successfully with the M51 vendor policy using the Android 30.0 compatibility mapping.

## 7. VINTF analysis

A71 and M51 VINTF manifests were compared by transport format, version, interface and instance.

The M51 FCM target level 5 was retained.

The level-5 development compatibility precheck found no explicit missing mandatory HAL requirement.

## 8. AVB test configuration

The original Samsung vbmeta descriptors could not validate modified partition contents.

A minimal test vbmeta with verification and hashtree disabled was created for first-boot development.

## 9. Recovery package

Full-block OTA payloads were generated for Hyper371 `system` and `product`.

Known-good M51 payloads are retained for `vendor` and `odm`.

M51 boot and DTBO are retained.

No modem or bootloader firmware is included in the v0.1 test installation flow.

## 10. Device preflight

Before first testing:

- hardware identity confirmed as `SM-M515F`
- firmware baseline confirmed as `M515FXXS6DXE3` / `RP6`
- dynamic partitions confirmed
- Download Mode confirmed
- `OEM LOCK: OFF (U)` confirmed
- custom recovery ADB confirmed
- EFS and `sec_efs` raw backups created and verified byte-for-byte

The project is currently at **first-boot testing**.

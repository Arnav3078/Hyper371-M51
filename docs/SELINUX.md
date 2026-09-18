# SELinux Compatibility

The Galaxy M51 vendor declares:

    plat_sepolicy_vers = 30.0

Hyper371 provides the corresponding compatibility mapping:

    /system/etc/selinux/mapping/30.0.cil
    /system/etc/selinux/mapping/30.0.compat.cil

The development port combines:

- Hyper371 platform policy
- Hyper371 product policy
- Hyper371 system_ext policy
- Galaxy M51 vendor policy

Offline `secilc` compilation completed successfully:

    secilc return code: 0
    SELINUX COMPILE: PASS

Generated test policy size was approximately 1.7 MiB.

## Precompiled policy note

The M51 ODM contains precompiled SELinux policy hashes that do not match the Hyper371 platform/product/system_ext policy hashes.

The project therefore does not assume the M51 precompiled policy blob can be reused unchanged.

## EROFS xattrs

After moving Hyper371 product and system_ext content into the M51 layout, required SELinux labels were restored before EROFS creation.

Verification used:

    fsck.erofs --xattrs --extract

Representative result:

    PASSED: 8
    FAILED: 0

Representative labels included Hyper371 services such as `qadaemon`, `hyos_spawner`, `miupdater`, `hypsys_system`, `miuibooster`, `qvirtmgr`, and `init.qti.display.sh`.

Permissive SELinux is not considered a final solution.

# Partition Architecture

## Dynamic group

Galaxy M51 dynamic group:

    qti_dynamic_partitions
    maximum size: 8048869376 bytes

Current v0.1 layout:

    remove_all_groups
    add_group qti_dynamic_partitions 8048869376
    add system qti_dynamic_partitions
    add vendor qti_dynamic_partitions
    add product qti_dynamic_partitions
    add odm qti_dynamic_partitions
    resize system 1435795456
    resize vendor 809484288
    resize product 2287689728
    resize odm 606208

Total allocation:

    4,533,575,680 bytes

Free space:

    3,515,293,696 bytes
    ~3352.45 MiB
    ~3.27 GiB

## Filesystems

The known-good M51 boot ramdisk expects EROFS for all four dynamic partitions:

    system   /system   erofs   logical,first_stage_mount
    product  /product  erofs   logical,first_stage_mount
    vendor   /vendor   erofs   logical,first_stage_mount
    odm      /odm      erofs   logical,first_stage_mount

There is no active standalone `system_ext` logical partition.

Hyper371 `system_ext` is stored at:

    /system/system_ext

with:

    /system_ext -> /system/system_ext
    /system/product -> /product

The root `/product`, `/vendor` and `/odm` paths remain mount points for their logical partitions.

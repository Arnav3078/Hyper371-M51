# Android Verified Boot

The original Galaxy M51 vbmeta is Samsung-signed and contains descriptors for the original partition contents.

Those descriptors cannot validate modified Hyper371 system/product images.

## Original M51 vbmeta

Original vbmeta:

    Algorithm: SHA256_RSA4096
    Flags: 0

## v0.1 test vbmeta

For first-boot development testing, a minimal vbmeta image was created with:

    Algorithm: NONE
    Flags: 3
    Descriptors: none

Flag meaning:

    1 = hashtree disabled
    2 = verification disabled
    3 = both disabled

This is an experimental development configuration and is not the intended security design for a mature release.

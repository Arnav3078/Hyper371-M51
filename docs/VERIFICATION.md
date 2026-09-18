# Verification Record

## system.img

    size: 1435795456 bytes
    SHA-256:
    6fc8c13abb275be5458d51cda178b410ecb48d4a06a466ab953c85b0bdcf3eb2

## product.img

    size: 2287689728 bytes
    SHA-256:
    65ce8e02b5ad1403363161f1a9c4e0cebb632c26404bb8988aed8a37d9818b1e

## M51 boot.img

    444897e443979214f9f00af38490b5968a870e32051357ec5d60d67e680c97a9

## M51 dtbo.img

    725c9f3839265555a58a67c2a41aa3bbeb320469da103a4fa8e8d66f1481cfd3

## Test vbmeta

    8f70c5b73592e5797c4fedf0d847550151d18f40810222dcec0a8e3209a6be33

## unsparse_super_empty.img

    23a9a8f401b7e2235ad5c903881d85e9d5c02866b43bc57fd8a2109383502305

## v0.1 test ZIP

    Hyper371_M51_v0.1_TEST.zip

    afdc447ca4453d4848a748da571229e3995213cef1ec4f9232053e67340b3a86

## EROFS

Both generated images passed `fsck.erofs`.

The generated EROFS feature set matched the known-good M51 reference style:

    SB_CHKSUM
    MTIME
    LZ4_0PADDING

## Payload

Brotli decompression of both generated `*.new.dat.br` files reproduced the exact original image hashes.

## Recovery ZIP

The final v0.1 test ZIP passed `unzip -t` with no compressed-data errors.

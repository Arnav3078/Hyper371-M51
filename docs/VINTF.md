# VINTF Compatibility

## Vendor target levels

Hyper371 A71 donor vendor:

    target-level="4"

Galaxy M51 vendor:

    target-level="5"

The M51 target level is intentionally retained rather than changed to match the donor.

## Framework matrices

Hyper371 contains framework compatibility matrices including:

    5
    6
    7
    8
    202404

## Important M51 HALs

Examples include:

    android.hardware.biometrics.fingerprint 2.1
    android.hardware.camera.provider 2.6
    android.hardware.radio 1.5
    android.hardware.radio.config 1.1
    android.hardware.sensors 2.0
    android.hardware.health 2.1
    android.hardware.wifi 1.4
    android.hardware.wifi.hostapd 1.2
    android.hardware.wifi.supplicant 1.3
    vendor.samsung.hardware.biometrics.fingerprint 3.0
    vendor.samsung.hardware.camera.provider 4.0
    vendor.samsung.hardware.radio 2.2

## A71 vs M51 differences

Notable hardware-specific differences include:

- A71 USB HIDL 1.3 vs M51 USB HIDL 1.1
- A71 Samsung Wi-Fi 2.3 vs M51 Samsung Wi-Fi 2.2
- A71 Samsung sysinput 1.3 vs M51 sysinput 1.2
- M51 NFC HALs are present where the A71 donor manifest differs
- M51 exposes an AIDL vibrator service

These differences are treated as device-specific and are not blindly replaced with donor declarations.

## Level-5 development precheck

The following Hyper371 matrices were examined:

    compatibility_matrix.5.xml
    compatibility_matrix.device.xml
    product/etc/vintf/compatibility_matrix.xml

Result:

    Mandatory FAIL      : 0
    Mandatory UNCHECKED : 0

Many optional framework HAL declarations are not implemented by the M51, which is expected for irrelevant hardware/platform capabilities.

This parser-based precheck is not equivalent to Google's official `checkvintf` implementation and must not be represented as formal VTS certification.

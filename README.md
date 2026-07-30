# HP Pavilion Gaming 15-dk0xxx Hackintosh EFI

OpenCore EFI for the **HP Pavilion Gaming 15-dk0xxx** running macOS Ventura.

## Hardware

| Component | Spec |
|---|---|
| CPU | Intel Core i5-9300H (Coffee Lake-H) |
| iGPU | Intel UHD Graphics 630 |
| dGPU | Nvidia GTX 1050 (disabled — not used) |
| RAM | 16GB |
| Storage | 500GB Samsung SSD |

## Status

| Feature | Status |
|---|---|
| Boot | ✅ Working |
| Graphics Acceleration (iGPU) | ✅ Working |
| Trackpad (I2C) | ✅ Working |
| Keyboard | ✅ Working |
| Audio | ✅ Working |
| Brightness Control | 🚧 In progress |
| Wi-Fi | ✅ Working |
| Bluetooth | ⚠️ Untested / not documented yet |
| Sleep/Wake | ✅ Working |

## ⚠️ Before You Boot

This EFI contains **placeholder SMBIOS values** (serial number, UUID, ROM, MLB).
**You must generate your own** before booting on real hardware — using
identical values to another machine can cause problems with iMessage/iCloud
and other Apple services.

1. Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
2. Run it and generate a new serial/UUID/ROM/MLB for SMBIOS model `MacBookPro15,1` (or whichever model this EFI targets — confirm in `config.plist` under `PlatformInfo`)
3. Replace the placeholder values in `EFI/OC/config.plist` under `PlatformInfo > Generic`

## Key Patches Used

- **Graphics**: `AAPL,ig-platform-id` set to `0x3EA50009` (device-id spoofed to `0x3E9B`), `-igfxblr` boot-arg required to prevent black screen on this board
- **Trackpad**: VoodooI2C + VoodooI2CELAN (ELAN I2C touchpad)
- **Audio**: AppleALC with `layout-id` — confirm your codec ID and adjust if audio doesn't work out of the box (see Issues)

## Known Issues

- Brightness keys / Control Center brightness slider not yet working — actively being worked on. See [Issues](../../issues).

## Credits

- Built with [HackMate](https://github.com/HackMate-OSX/HackMate) plus a good amount of manual patching/troubleshooting
- Uses [OpenCore](https://github.com/acidanthera/OpenCorePkg) and the [Acidanthera](https://github.com/acidanthera) kext ecosystem
- Trackpad and PS2 support via [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) and [VoodooPS2](https://github.com/acidanthera/VoodooPS2)

## Disclaimer

Use at your own risk. This is a community-built, unofficial configuration and
is not affiliated with HP, Apple, or Intel.

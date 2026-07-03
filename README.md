# ThinkPad X1 Carbon 6th Hackintosh EFI

Language: **English** | [简体中文](README.zh-CN.md)

This repository archives two tested EFI sets for the Lenovo ThinkPad X1 Carbon 6th.

Tested macOS versions:
- `EFI-Ventura13-stable-RMI-20260610-1438` on macOS 13.7.6
- `EFI-Sequoia15-stable-itlwm-HeliPort-20260610-234402` on macOS 15.7.5

These archives are machine-specific and were verified on this exact ThinkPad. They are not guaranteed for other BIOS revisions, hardware swaps, or later macOS point releases.

## Warning 
- There are some issues with audio layout that may cause audio distortion,additional latency,poping sounds,and other problems.
- another issues, when your device has been in sleep mode for too long, it will be reboot and display

`0251:System CMOS Checksum bad - Default configuration used.

I try to change plist but it not work

I've already sold this laptop so, Good luck for you lol.

## What works

- Graphics
- Audio
- Battery
- Sleep and wake
- Keyboard
- Trackpad and TrackPoint
- Bluetooth
- Ethernet
- USB and Thunderbolt layout based on Tyler Nguyen's X1C6 ACPI work

## EFI variants

### macOS 13.7.6 archive

- Uses `AirportItlwm.kext`
- `itlwm.kext` removed from this copy
- Intended for the Ventura branch

### macOS 15.7.5 archive

- Uses `itlwm.kext` + HeliPort
- `AirportItlwm.kext` removed from this copy
- Intended for the Sequoia branch

In this setup, `itlwm + HeliPort` was more reliable on macOS 15. `AirportItlwm` could boot, but Wi-Fi was not usable on this machine.

## USB, Thunderbolt, and ACPI

This repository does not use `USBToolBox.kext` or `UTBDefault.kext`.
The USB and Thunderbolt layout comes from the same ACPI approach used by Tyler Nguyen for the X1C6:

- `SSDT-XHC1.aml`
- `SSDT-TB-DSB0.aml` through `SSDT-TB-DSB6.aml`
- `SSDT-TB-DSB2-XHC2.aml`

The bundled ACPI tables match the upstream Tyler X1C6 repository byte-for-byte for those files.

`ECEnabler.kext` was removed from both archives. Battery handling is done through ACPI plus `SMCBatteryManager.kext`.

## Usage

1. Pick the archive that matches your macOS version.
2. Copy the `EFI` folder to your ESP.
3. Back up your existing EFI first.
4. Do not mix the Ventura Wi-Fi kext set with the Sequoia one.
5. Recheck sleep and wake after any USB or Thunderbolt change.

## Disclaimer

This repository is provided for personal archival, research, and educational purposes only.

- Use it at your own risk.
- No warranty is provided.
- The author is not responsible for data loss, boot failure, hardware issues, macOS update problems, account issues, or any other damage caused directly or indirectly by using this EFI.
- This repository does not include macOS, macOS installers, recovery images, or any Apple copyrighted operating system files.
- Please follow the licenses and terms of Apple, OpenCore, and all referenced third-party projects.
- This archive is not commercial support and does not promise compatibility with your device.

## Notes

- `USBToolBox.kext` removed
- `UTBDefault.kext` removed
- `ECEnabler.kext` removed
- This is an archive, not a universal X1C6 EFI for every BIOS or macOS revision

## Thanks and references

This repository was built with direct reference to:

- Tyler Nguyen X1C6 guide: https://tylernguyen.github.io/x1c6-hackintosh/installing-macOS/
- Tyler Nguyen X1C6 repository: https://github.com/tylernguyen/x1c6-hackintosh
- OpenCorePkg: https://github.com/acidanthera/OpenCorePkg
- OpenIntelWireless itlwm: https://github.com/OpenIntelWireless/itlwm
- OpenIntelWireless HeliPort: https://github.com/OpenIntelWireless/HeliPort
- Lilu: https://github.com/acidanthera/Lilu
- WhateverGreen: https://github.com/acidanthera/WhateverGreen
- VirtualSMC: https://github.com/acidanthera/VirtualSMC
- AppleALC: https://github.com/acidanthera/AppleALC
- IntelBluetoothFirmware: https://github.com/OpenIntelWireless/IntelBluetoothFirmware
- VoodooPS2Controller: https://github.com/acidanthera/VoodooPS2
- VoodooRMI / VoodooSMBus: https://github.com/VoodooSMBus/VoodooRMI

Thanks to Tyler Nguyen and the maintainers of the projects above for the documentation, ACPI work, and drivers that made this archive possible.

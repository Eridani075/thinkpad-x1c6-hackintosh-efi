# ThinkPad X1 Carbon 6th Hackintosh EFI

Language: [English](README.md) | **简体中文**

这个仓库收录了 Lenovo ThinkPad X1 Carbon 6th 的两份 EFI 归档。

已测试的 macOS 版本：
- `EFI-Ventura13-stable-RMI-20260610-1438` 测试于 macOS 13.7.6
- `EFI-Sequoia15-stable-itlwm-HeliPort-20260610-234402` 测试于 macOS 15.7.5

这两套 EFI 都是针对这台机器调好的，并且在归档时确认可用。但它们不保证适用于其他 BIOS 版本、硬件变动，或者更后的 macOS 小版本。

## 一些问题
audio layout可能需要自己折腾一下 目前这个layout在插耳机大音量状况下会失真破音 外放还没试 我机器已经卖了 你们自己尝试罢（x

## 已验证功能

- 显卡
- 声卡
- 电池
- 睡眠与唤醒
- 键盘
- 触控板和小红点
- 蓝牙
- 有线网卡
- 基于 Tyler Nguyen X1C6 ACPI 思路的 USB / Thunderbolt 布局

## 两套 EFI 的差异

### macOS 13.7.6 归档

- 使用 `AirportItlwm.kext`
- 已从这个副本里移除 `itlwm.kext`
- 适合 Ventura 分支

### macOS 15.7.5 归档

- 使用 `itlwm.kext` + HeliPort
- 已从这个副本里移除 `AirportItlwm.kext`
- 适合 Sequoia 分支

在这台机器上，macOS 15 下 `itlwm + HeliPort` 更稳定；`AirportItlwm` 虽然能启动，但无线不可用。

## USB、雷电与 ACPI

本仓库没有使用 `USBToolBox.kext` 或 `UTBDefault.kext`。
USB 和 Thunderbolt 的布局主要来自 Tyler Nguyen 的 X1C6 ACPI 方案：

- `SSDT-XHC1.aml`
- `SSDT-TB-DSB0.aml` 到 `SSDT-TB-DSB6.aml`
- `SSDT-TB-DSB2-XHC2.aml`

仓库中的这些 ACPI 表与 Tyler X1C6 仓库对应文件是逐字节一致的。

`ECEnabler.kext` 也已从两套归档里移除。电池管理由 ACPI 配合 `SMCBatteryManager.kext` 完成。

## 使用方法

1. 根据 macOS 版本选择对应 EFI。
2. 将 `EFI` 文件夹复制到 ESP。
3. 覆盖前先备份原 EFI。
4. 不要混用 Ventura 和 Sequoia 的 Wi-Fi kext。
5. 任何 USB 或 Thunderbolt 调整后，都建议重新检查睡眠和唤醒。

## 免责声明

本仓库仅用于个人归档、研究和学习目的。

- 使用风险由使用者自行承担。
- 本仓库不提供任何形式的保证。
- 因使用本 EFI 直接或间接造成的数据丢失、无法启动、硬件异常、系统更新问题、账号问题或其他损失，作者不承担责任。
- 本仓库不包含 macOS 系统本体、macOS 安装器、恢复镜像或任何 Apple 受版权保护的操作系统文件。
- 请自行遵守 Apple、OpenCore 以及所有引用第三方项目的许可和条款。
- 本仓库不是商业支持，也不承诺适配你的设备。

## 调试过程摘要

这两份 EFI 的整理过程主要经历了这些验证：

1. 先确认 13 和 15 两份 EFI 的稳定版本可以正常启动。
2. 分别测试 Intel Wi-Fi 的两条路线：
   - Ventura 用 `AirportItlwm`
   - Sequoia 用 `itlwm + HeliPort`
3. 经过多轮测试后确认 `AirportItlwm` 在 macOS 15 上无法稳定得到可用 Wi-Fi。
4. 对比 Tyler Nguyen 的 X1C6 仓库后确认，当前 EFI 已经在使用他那套 ACPI 思路。
5. 进一步比对后发现，仓库中的 `SSDT-XHC1.aml` 和 `SSDT-TB-DSB2-XHC2.aml` 与 Tyler 仓库对应文件逐字节一致。
6. 因此不再引入 `USBToolBox.kext` / `UTBDefault.kext`，也不再修改这套已经成熟的 USB / Thunderbolt 映射。
7. 最后清理了没启用且不再需要的 `ECEnabler.kext`、`USBToolBox.kext` 和 `UTBDefault.kext`。

## 说明

- `USBToolBox.kext` 已移除
- `UTBDefault.kext` 已移除
- `ECEnabler.kext` 已移除
- 这是归档版本，不是面向所有 BIOS 和所有 macOS 版本的通用 X1C6 EFI

## 参考与感谢

本仓库制作过程中参考并使用了以下项目与文档：

- Tyler Nguyen X1C6 安装文档：https://tylernguyen.github.io/x1c6-hackintosh/installing-macOS/
- Tyler Nguyen X1C6 仓库：https://github.com/tylernguyen/x1c6-hackintosh
- OpenCorePkg：https://github.com/acidanthera/OpenCorePkg
- OpenIntelWireless itlwm：https://github.com/OpenIntelWireless/itlwm
- OpenIntelWireless HeliPort：https://github.com/OpenIntelWireless/HeliPort
- Lilu：https://github.com/acidanthera/Lilu
- WhateverGreen：https://github.com/acidanthera/WhateverGreen
- VirtualSMC：https://github.com/acidanthera/VirtualSMC
- AppleALC：https://github.com/acidanthera/AppleALC
- IntelBluetoothFirmware：https://github.com/OpenIntelWireless/IntelBluetoothFirmware
- VoodooPS2Controller：https://github.com/acidanthera/VoodooPS2
- VoodooRMI / VoodooSMBus：https://github.com/VoodooSMBus/VoodooRMI

感谢 Tyler Nguyen 和上述项目的维护者提供的文档、ACPI 方案和驱动支持。

Ventura 13 stable EFI archive for ThinkPad X1 Carbon 6th.

Archived: 2026-06-10 14:38 Asia/Shanghai
Source: EFI-Tyler-RMI-test-20260610-142401

Known-good status reported by user:
- Boots macOS Ventura 13.
- Touchpad is much more responsive with Tyler-style VoodooRMI + VoodooSMBus.
- Sleep had already been verified after prior tuning.

Input stack:
- VoodooSMBus.kext enabled.
- VoodooRMI.kext enabled.
- VoodooRMI RMISMBus plugin enabled.
- VoodooRMI RMII2C plugin disabled.
- VoodooPS2Controller.kext enabled.
- VoodooPS2Keyboard.kext enabled.
- VoodooPS2Mouse.kext disabled.
- VoodooPS2Trackpad.kext disabled.

Do not modify this archive directly. Use it as the rollback baseline before
building Sequoia/macOS 15 test EFIs.

macOS 15 Sequoia test EFI, legacy/stable OpenCore build.

Created from EFI-Ventura13-stable-RMI-20260610-1438 after the OpenCore 1.0.7 test failed before the OC picker.

Changes from Ventura 13 stable baseline:
- Keep the known-good BOOTx64.efi, OpenCore.efi, OpenRuntime.efi, ResetNvramEntry.efi, and config schema.
- Keep the working Tyler-style VoodooSMBus + VoodooRMI/RMISMBus input stack.
- Keep AirportItlwm.kext limited to Ventura kernel 22.x.
- Add itlwm.kext 2.3.0 limited to Sequoia kernel 24.x; use HeliPort app on macOS 15.

Purpose:
- Restore OC picker bootability first, then test Ventura 13 and future Sequoia upgrade path.

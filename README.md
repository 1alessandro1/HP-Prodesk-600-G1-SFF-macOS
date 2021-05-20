# HP Prodesk 600-G1 SFF - iMac15,1

This repository contains the necessary files and information to successfully boot macOS on this prebuilt PC. 
- Bootloader version: **OpenCore 0.6.9**
- Kexts version: everything up-to-date with the latest version (check the links below)
- Current macOS version: [Big Sur 11.3.1](https://www.apple.com/macos/big-sur) - Release channel
- With a different SMBIOS, e.g. `iMac14,4` you [can install](https://youtu.be/o6cdezPEF3A) up to OS X Mavericks (10.9) 

## Specs

| Component      | Brand                                     |
|----------------|-------------------------------------------|
| **CPU**        | `Intel Core i5-4590 @ 3.3 GHz`            |
| **Chipset**    | `Intel Q85`                               |
| **iGPU**       | `Intel HD Graphics 4600 - Haswell`        |
| **Storage**    | `Crucual NVMe 250GB`                      |
| **Audio**      | `Realtek ALC221 - layout 11`              |
| **Ethernet**   | `Intel I217LM`                            |
| **OS**         | `macOS Big Sur 11.3.1 (20E241)`           |
| **BIOS**       | `2.78 - 29 April 2020`                    |

## Important notes
- In the `config.plist`, section `PlatformInfo > Generic`, the following fields are currently edited with "CHANGEME" in order to force the user to generate his own serials. Refer to this guide to [know how](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo). 
  - `MLB`
  - `ROM`
  - `SystemSerialNumber` 
  - `SystemUUID`

- If you are planning an NVMe device on the PCI-E x16 or x1 slots, note that on Aptio IV firmware, NvmeExpressDxe is not present, check the `Drivers/` folder under `EFI/OC/` path of this repository, and don't forget to add `NvmeExpressDxe.efi` that to the `ConnectDrivers` section in OpenCore's `config.plist`. If you don't plan to use an NVMe, you can skip this and remove NvmeExpressDxe from the `Drivers/` folder and from the `config.plist`


## BIOS Settings

There are screenshots to document what are the necessary BIOS settings for this PC, check them [here](https://github.com/1alessandro1/HP-Prodesk-600-G1-SFF-macOS/tree/main/Bios-Dumps/Pictures-Settings) or by cloning the repository 

## Additional hidden BIOS settings
The tool `setup_var` from [datasone](https://github.com/datasone/grub-mod-setup_var/releases/latest) can help you to setup this additional parameters to successfully boot macOS:

Instructions: copy `modGRUBShell.efi` to a FAT32 partition and save it under the directory `ESP/EFI/BOOT/` as `BOOTx64.efi`, your firmware will target that `.efi` driver to boot, and once you reached the GRUB command line, type the following (these offsets apply to this firmware in particular with this BIOS version, 2.78)

- CFG Lock: `setup_var 0x4A3 0x00` [Disabled]
- DVMT GFX total mem: `setup_var 0x234 0x3` [MAX]
- EHCI Hand-off: `setup_var 0x2 0x1` [Enabled]
- Serial ports: [Disable All]
  - (Serial Port A) `setup_var 0x13 0x00`
  - (Serial Port B) `setup_var 0x15 0x00`
  - (Serial Port C) `setup_var 0x17 0x00`
  - (Serial Port D) `setup_var 0x19 0x00`

Unfortunately I was not able to unlock the `DVMT Pre-Allocated` (offset `0x233`) in order to increse it from `32MB` to someting higher like `64MB` or `128MB` as discussed [here](https://github.com/acidanthera/bugtracker/issues/1585) so the max achievable resolution is *QHD*, `2560x1440` with the iGPU under macOS, but in Linux/Windows everythig is correct even at `3840x2160`

**Note**: if you don't apply the correct BIOS settings, you won't be able to boot.

### Drivers

Must have to boot Big Sur:

* OpenRuntime.efi (bundled in OpenCore package)
* And nothing else (if you created the USB with [this method](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install-recovery.html#legacy-macos-online-method))

For USB creation methods which use `createinstallmedia`, any version of macOS (Big Sur, Catalina etc) may require add: 

* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) (in order to let OpenCore see the HFS partition created by the tool)


### Kexts

* [AppleALC](https://github.com/acidanthera/AppleALC/releases/latest)
* [CPUFriend](https://github.com/acidanthera/CPUFriend/releases/latest)
* [Lilu](https://github.com/acidanthera/Lilu/releases/latest)
* [NVMeFix](https://github.com/acidanthera/NVMeFix/releases/latest)
* [IntelMausi](https://github.com/acidanthera/IntelMausi/releases/latest)
* [SMCProcessor](https://github.com/acidanthera/VirtualSMC/releases/latest) - shipped inside **VirtualSMC**
* [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases/latest) 
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases/latest)

## Credits:

* [Apple](https://apple.com) for macOS
* [Mieze](https://github.com/Mieze) for IntelMausi LAN driver
* [dreamwhite](https://github.com/dreamwhite) for helping me with `SSDT-USB.aml` which does not require DSDT patching
* [Gengik84](https://www.macos86.it/profile/1-gengik84/) for the `GENG` method and for the original custom DSDT
* [dortania](https://github.com/dortania) team for its detailed guides
* [Corpnewt](https://github.com/CorpNewt) for SSDTTime and [fewtarius](https://github.com/fewtarius) for CPUFriend fork
* [Acidanthera](https://github.com/Acidanthera) for OpenCore and Lilu-based kexts 

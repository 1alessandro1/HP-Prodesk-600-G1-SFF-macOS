# HP-Prodesk-600-G1-SFF-macOS
This repository contains the necessary files and information to successfully boot macOS on this prebuilt PC. 

## Specs

| Component      | Brand                                     |
|----------------|-------------------------------------------|
| **CPU**        | `Intel Core i5-4590 @ 3.3 GHz`            |
| **Chipset**    | `Intel Q85`                               |
| **iGPU**       | `Intel HD Graphics 4600 - Haswell`        |
| **Storage**    | `Crucual NVMe 250GB`                      |
| **Audio**      | `Realtek ALC221 - layout 11`              |
| **Ethernet**   | `Intel I217LM`                            |
| **OS**         | `macOS Big Sur 11.2.3 (20D91)`            |
| **BIOS**       | `2.78 - 29 April 2020`                    |

## Additional hidden BIOS settings
The tool `setup_var` from [datasone](https://github.com/datasone/grub-mod-setup_var/releases/latest) can help you to setup this additional parameters to successfully boot macOS:

Instructions: copy `modGRUBShell.efi` to a FAT32 partition and save it under the directory `ESP/EFI/BOOT/` as `BOOTx64.efi`, your firmware will target that `.efi` driver to boot, and once you reached the GRUB command line, type the following (these offsets apply to this firmware in particular with this BIOS version, 2.78)


- CFG Lock: `setup_var 0x4A3 0x00` [Disabled]
- DVMT GFX total mem: `setup_var 0x234 0x3` [MAX]
- EHCI Hand-off: `setup_var 0x2 0x1` [Enabled]

Unfortunately I was not able to unlock the `DVMT Pre-Allocated` (offset `0x233`) in order to increse it from `32MB` to someting higher like `64MB` or `128MB` as discussed [here](https://github.com/acidanthera/bugtracker/issues/1585)

Note: if you don't apply the correct BIOS settings, you won't be able to boot.

* [Apple](https://apple.com) for macOS
* [Acidanthera](https://github.com/Acidanthera) for some Lilu-based kexts
* [dreamwhite](https://github.com/dreamwhite) for helping me with `SSDT-USB.aml` which does not require DSDT patching
* [Gengik84](https://www.macos86.it/profile/1-gengik84/) for the `GENG` method and for the original custom DSDT
* [dortania](https://github.com/dortania) team for its detailed guides
* [Corpnewt](https://github.com/CorpNewt) for SSDTTime and [fewtarius](https://github.com/fewtarius) for CPUFriend fork
* [Mieze](https://github.com/Mieze) for IntelMausi LAN driver

# HP-Prodesk-600-G1-SFF-macOS
This repository contains the necessary files and information to successfully boot macOS on this prebuilt PC. 

## Specs

| Component      | Brand                                     |
|----------------|-------------------------------------------|
| **CPU**        | `Intel Core i5-4590 @ 3.3 GHz`            |
| **iGPU**       | `Intel HD Graphics 4600 - Haswell`        |
| **Storage**    | `Crucual NVMe 250GB`                      |
| **Audio**      | `Realtek ALC221 - layout 11`              |
| **Ethernet**   | `Intel I217LM`                            |
| **OS**         | `macOS Big Sur 11.2.3 (20D91)`            |
| **BIOS**       | `2.78 - 29 April 2020`                    |

## Additional hidden BIOS settings
The tool `setup_var` from [datasone](https://github.com/datasone/grub-mod-setup_var/releases/latest) can help you to setup this additional parameters to successfully boot macOS:

- CFG Lock: `setup_var 0x4A3 0x00` [Disabled]
- DVMT GFX total mem: `setup_var 0x234 0x3` [MAX]
- EHCI Hand-off: `setup_var 0x2 0x1` [Enabled]

Note: if you don't apply the correct BIOS settings, you won't be able to boot.

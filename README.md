# HP-Prodesk-600-G1-SFF-macOS
This repository contains the necessary files and information to successfully boot macOS on this prebuilt PC. 

## Additional hiddein BIOS settings
The tool `setup_var` from [datasone](https://github.com/datasone/grub-mod-setup_var/releases/latest) can help you to setup this additional parameters to successfully boot macOS:

- CFG Lock: `setup_var 0x4A3 0x00` [Disabled]
- DVMT GFX total mem: `setup_var 0x234 0x3` [MAX]
- EHCI Hand-off: `setup_var 0x2 0x1` [Enabled]

Note: if you don't apply the correct BIOS settings, you won't be able to boot.

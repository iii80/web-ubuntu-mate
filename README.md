# Ubuntu Tiny: A Fast, Portable and Power-Saving edition for Ubuntu/Debian LTS

------------------------------------------
### What's New:

* 20250504: Debian 13 Trixie Draft (aarch64 + amd64);
* 20241225: Bug Fix - EFI dependency missing using Wiminstall.gptboot for Windows Installation;
* 20241116: Add Ubuntu Tiny for Arm64 (support [Mac VBox](https://www.virtualbox.org/wiki/Downloads) / Android pKVM);
* 20241027: Update virtio_gpu detection for QEMU; Add cmd "mount.ios" for Iphone;
* 20240818: Allow "Boot in normal mode" if booting from Ventoy;
* 20240704: Enable "Alt + PrtScr" for Area Screenshot;
* 20240425: Ubuntu Tiny 24.04 Stable;
* 20240407: Security Packs for Ubuntu 24.04 (beta);
* 20240316: Upgrade to Linux 6.8 + Python 3.12.2;
* 20240224: Second Edition of Ubuntu 24.04 Tiny;
* 20230312: Include Ubuntu Monthly Security Packs;
* 20230121: Add Onboard for Touchscreen; Add Resource Indicator to Panel;
* 20230108: Add Hivex Windows Registry Editor and NT Password Tools;
* 20221225: Fix Desktop-Icon Disappearance after Login; Upgrade Integrated Web Paint;
* ..

------------------------------------------

### - Ubuntu Tiny 24.04 Noble LTS for CDROM/USB (LANG = en_US | zh_CN):

>
>
> **Download Full Desktop Version (560M+)**: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-24.04/noble-mate-x86_64-20241225.iso) | [arm64 (UEFI)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-24.04/noble-mate-aarch64-20241225.iso)
>
> **Download No-desktop Version (140M+)**: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-24.04/noble-core-x86_64-20241122.iso) | [arm64 (UEFI)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-24.04/noble-core-aarch64-20241122.iso)

### - Debian Tiny 13 Trixie for CDROM/USB (LANG = en_US | zh_CN):

> **Download Full Desktop Version (550M+)**: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/debian-13/trixie-mate-x86_64-20250421.iso) | [arm64 (UEFI)](https://github.com/ghostplant/ubuntu-pe/releases/download/debian-13/trixie-mate-aarch64-20250421.iso)

<p align="center">
  <img src="Ubuntu_PE.jpg" data-canonical-src="Ubuntu_PE.jpg" />
</p>

------------------------------------------

### - Early Versions in History:

- **Debian 12 Tiny (LANG = en_US | zh_CN)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/debian-12/debian-mate-x86_64-20231220.iso) | [x86 (MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/debian-12/debian-mate-i686-20231226.iso)

- **Ubuntu 22.04 LTS Tiny (LANG = en_US | zh_CN)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-22.04/jammy-mate-x86_64-20231220.iso)

- **Ubuntu 22.04 LTS Tiny Core (LANG = en_US)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-22.04/jammy-core-x86_64-20221015.iso)

- **Ubuntu 20.04 LTS Tiny (LANG = en_US | zh_CN)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-20.04/focal-mate-x86_64-20221002.iso)

- **Ubuntu 18.04 LTS Tiny (LANG = en_US | zh_CN, No WimTool)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-18.04/bionic-mate-amd64-20200222.iso) | [x86 (MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-18.04/bionic-mate-i386-20200222.iso)

- **Ubuntu 16.04 LTS Tiny (LANG = en_US | zh_CN, No WimTool)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-18.04/xenial-classic-amd64-20231217.iso)

- **Ubuntu 10.04 LTS Tiny (LANG = en_US | zh_CN, No WimTool)** Download: [x64 (UEFI+MBR)](https://github.com/ghostplant/ubuntu-pe/releases/download/ubuntu-18.04/maverick-classic-amd64.iso)

------------------------------------------

   *1. Write Ubuntu Tiny ISO to USB:*

       sudo dd if=./focal-mate-x86_64-xxxxxxxx.iso of=/dev/<usb-dev-file> bs=16K && sync

   *2. Ubuntu Tiny Supported Features (Only for Ubuntu 20.04, 22.04 and future versions):*
   
       1. Support Booting USB/CDROM in both MBR & UEFI machines;

       2. Support Installing Ubuntu Image to Hard Drive: sudo ubi-lite

       3. Support Installing Windows Image to MBR Hard Drive: sudo wiminstall.mbrboot /dev/<os-part-name> <WIM file> <image-id>

           [Method-1: Will Erase Grub in Hard drive (cautious!)]
           ex-1: sudo wiminstall.mbrboot /dev/sda1 ./xp-sp3.wim
           ex-2: sudo wiminstall.mbrboot /dev/sda1 ./windows-7.wim 4
           ex-3: sudo wiminstall.mbrboot /dev/sda1 ./windows-11.wim 1

           [Method-2: Not Erase Grub in Hard drive, but need three-step manual configuration on boot settings]
           step-1: Ensure Ubuntu + Grub has been installed on hard driver partitions other than /dev/sda1
           step-2: sudo wiminstall /dev/sda1 ./xp-sp3.wim
           step-3: Reboot, login Ubuntu and run: sudo update-grub
           
           [Method-3: For UEFI Installation to GPT Hard Drive]
           sudo EFI=/dev/<efi-part-name> wiminstall.gptboot /dev/<os-part-name> <WIM file> <image-id>

------------------------------------------

### Ubuntu Tiny Desktop for Remote Internet:
(Default VNC password: 123456, and you can update it via 'vncpasswd' command inside VNC X session)

```sh
# Download/Update latest Ubuntu image
docker pull ghostplant/flashback

# Boot Service: Using web browser to login - http://localhost:8443/
docker run -it --rm --privileged -p 8443:8443 -v /external:/root ghostplant/flashback

# Other Example 1 - Language: Set locale to en_US.UTF-8
docker run -it --rm --privileged -e LANG=en_US.UTF-8 -p 8443:8443 -p 5901:5901 -v /external:/root ghostplant/flashback

# Other Example 2 - Resolution Size : Set display resolution to 1366x768
docker run -it --rm --privileged -e GEOMETRY=1366x768 -p 8443:8443 -p 5901:5901 -v /external:/root ghostplant/flashback

# Other Example 3 - Initial Password: Set initial VNC password (length of password must be between 6 to 8).
docker run -it --rm --privileged -e INIT_PASS=123456 -p 8443:8443 -p 5901:5901 -v /external:/root ghostplant/flashback

# Other Example 4 - Resolution Quality: Using 24-bit high resolution quality (Only recommended in high-bandwidth network)
docker run -it --rm --privileged -e INIT_PASS=123456 -e DEPTH=24 -p 8443:8443 -p 5901:5901 -v /external:/root ghostplant/flashback
```

Then use Firefox/Chrome to login if you expose port 8443:

```sh
HTTP: x-www-browser http://localhost:8443/

HTTPS: x-www-browser https://localhost:8443/
```

------------------------------------------

## Reporting Issues

You can post issues here for any suggestions to improve Ubuntu Classic Desktop. To report a new issue, you are supposed to have a GitHub account and log in with it in the first place. Then, get access to [new issue](https://github.com/ghostplant/ubuntu-classic/issues/new), fill in the block with what you want to report, and finally submit this issue.

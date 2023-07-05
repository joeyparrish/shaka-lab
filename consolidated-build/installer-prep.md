# Shaka Lab Consolidated Build Instructions - Installer Prep

While the Ubuntu installer ISO can be imaged directly to a thumb drive with
`dd`, the Windows installer ISO cannot.  To solve this, we use a tool called
Ventoy that will allow us to drop ISO images onto a filesystem on the thumb
drive, then boot those indirectly.  It even allows multiple ISOs, so we can
have a single installer drive for both Linux and Windows.  (As of 2023, these
two installers will require a minimum thumb drive size of 8GB.  If you need a
third installed for Arm Linux devices, you will need at least 10GB.)

1. Download Ubuntu Server 22.04 LTS:
   https://releases.ubuntu.com/22.04.2/ubuntu-22.04.2-live-server-amd64.iso
2. If you have arm devices, download Ubuntu Server 22.04 LTS for Arm:
   https://cdimage.ubuntu.com/releases/22.04/release/ubuntu-22.04.2-live-server-arm64.iso
3. Download a Windows 11 ISO file from Microsoft:
   https://www.microsoft.com/software-download/windows11
4. Download Ventoy:
   https://github.com/ventoy/Ventoy/releases
5. Unpack Ventoy (assuming Linux host):
   ```sh
   cd Downloads
   tar xf ventoy-*-linux.tar.gz
   ```
6. Run Ventoy (assuming Linux host):
   ```sh
   cd ventoy-*
   ./VentoyGUI.x86_64
   ```
7. Select your USB thumb drive under "Device".  (If it's not plugged in already,
   plug it in, then hit the "reload" button, then select it.)
8. Click "Install".
9. Mount the USB device (use "Files" app if you aren't familiar with the
   command line).
10. Copy both the Ubuntu and Windows ISO files to the USB device.
11. Unmount/eject the device.

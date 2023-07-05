# Shaka Lab Consolidated Build Instructions - Windows

If you haven't yet prepared an installer, please read
[Installer Prep](installer-prep.md).

Please refer to [Devices](devices.md) for any hardware-specific pre-install
setup and for a list of packages for this device.


## OS Installation

1. Insert the flash drive into the new Windows device and power it on.
2. Enter the boot menu (press F11 on Topaz 2).
3. Select the USB drive (may say "UEFI") and then "Windows".
4. Select "boot in normal mode".
5. Get a Windows product key from
   [Visual Studio Subscriptions](https://visualstudio.microsoft.com/subscriptions/)
   (inside Google, see go/vanilla-windows for subscription information)
   1. Where it says "Benefits" in the top-left, change to "Product Keys".
   2. Search for "Windows 11 Professional".
   3. Click "Claim Key" or copy a key you have already claimed.
6. When prompted, enter the product key in the installer.
7. If reinstalling, choose "Install Windows Only" to wipe the old installation,
   then format the primary partition.
8. The system will automatically reboot during installation.
9. After setting language, keyboard layout, and hostname, the system will
   reboot again.
10. Choose "Set up for personal use".
11. Click "Sign in".
12. Enter the email "no@thank.you" and any password.
13. After failing to sign in, you'll be given the option for a local login.
14. When prompted to "Enter your name", use the account name and password.
    stored in the Google-internal password manager under "Shaka Lab Default
    Login".
15. When prompted for privacy settings, disable all options.


## Setup

1. Open settings and search for "update".
2. Click "Check for updates".
3. Wait for updates and drivers to install.
4. If prompted to restart after updates, click "Restart now".
5. Click the search field in the taskbar and type "powershell".
6. Right-click "Windows PowerShell" and select "Run as administrator"
7. Copy the PowerShell command from the
   [official Chocolatey installation instructions](https://chocolatey.org/install#individual).
8. Right-click in PowerShell to paste the command, then press enter.
9. Set up access to the Shaka Lab packages by running this command:
   ```ps1
   choco source add -n=shaka-lab -s=https://shaka-lab-chocolatey-dot-shaka-player-demo.appspot.com/
   ```
10. For each package in the list for this machine, run:
    ```ps1
    choco install -y PACKAGE-NAME-GOES-HERE
    ```
11. Edit `c:/ProgramData/shaka-lab-node/shaka-lab-node-config.yaml` to
    configure this node's browsers.
12. Restart the service:
    ```ps1
    net stop shaka-lab-node
    net start shaka-lab-node
    ```

# Shaka Lab Consolidated Build Instructions - macOS

**NOTE**: There is no installer media or prep for macOS.

Please refer to [Devices](devices.md) for any hardware-specific pre-install
setup and for a list of packages for this device.


## OS Installation

1. Erase your mac and reset it to factory settings:
   https://support.apple.com/en-us/HT212749
2. Boot into the macOS installer
3. When prompted for WiFi, select "Other Network Options" in the bottom-left,
   then "Local network (Ethernet)".
4. When prompted for migration assistant, select "Not Now" in the bottom-left.
5. Log in with an Apple ID:
   1. Inside Google: Log in with the shared Shaka Apple ID and password stored
      in the Google-internal password manager under "Shaka Lab Apple ID".
   2. Outside Google: Log in with your preferred Apple ID.
6. When prompted to "Create a Computer Account", use the account name and
   password stored in the Google-internal password manager under "Shaka Lab
   Default Login".
7. When prompted for "Screen Time", select "Set Up Later" in the bottom-left.
8. When prompted for "Siri", uncheck "Enable Ask Siri".
9. When prompted for "FileVault Disk Encryption", uncheck "Turn on FileVault
   disk encryption".


## Setup

1. Grant full disk access to Terminal.  Without this, package installation
   scripts for shaka-lab-recommended-settings will be unable to make changes to
   OS settings.
   1. Click the Apple icon in the top-left of the screen.
   2. Click "System Preferences".
   3. Search "privacy" and select "Privacy settings".
   4. Click the lock icon and enter your password.
   5. Scroll down and click "Full Disk Access".
   6. Click the plus icon on the right half of the dialog.
   7. Select "Applications" > "Utilities" > "Terminal", then click "Open".
   8. If Terminal is open, click "Quit & Reopen".
2. Open Terminal (Finder > Applications > Utilities) and run the following
   command:
   ```sh
   installer="https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh"
   bash -c "$(curl -fsSL $installer)"
   ```
3. When the command is finished, there will be two more commands in the output
   under the heading "**==> Next steps**".  Copy and paste those into the
   terminal.
4. Set up access to the Shaka Lab packages by running this command:
   ```sh
   brew tap homebrew/cask-versions
   brew tap shaka-project/shaka-lab
   ```
5. For each package in the list for this machine, run:
   ```sh
   # NOTE: Reboot after shaka-lab-recommended-settings and before
   # shaka-lab-node if nobody is logged in on the GUI!  Autologin is required
   # and someone must be logged in when installing shaka-lab-node.
   brew install PACKAGE-NAME-GOES-HERE
   ```
6. Edit `/etc/shaka-lab-node-config.yaml` to configure this node's browsers.
7. Restart the service:
   ```sh
   sudo /opt/shaka-lab-node/restart-services.sh
   ```

# Shaka Lab Consolidated Build Instructions - Devices

## Overview

This is an overview of **our** lab devices, their hardware, their OSes, and the
packages we install.  Your lab may vary.

Items in **bold** are meant to draw your attention to packages and configs that
are relatively unusual compared to the other devices.

 - shaka-lab-gateway ([Topaz 2 NUC 12][], running Ubuntu 22.04 LTS)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - **shaka-lab-gateway**
 - shaka-test-linux ([Topaz 2 NUC 12][], running Ubuntu 22.04 LTS)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - shaka-lab-browsers
   - shaka-lab-node
     - **browsers: chrome-android, chromecast, tizen**
   - **shaka-lab-hub**
   - **shaka-lab-certs**
   - **shaka-lab-github-runner**
 - shaka-test-linux2 ([Topaz 2 NUC 12][], running Ubuntu 22.04 LTS)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - shaka-lab-browsers
   - shaka-lab-node
     - **browsers: chrome, firefox, edge**
 - shaka-test-windows ([Topaz 2 NUC 12][], running Windows)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - shaka-lab-browsers
   - shaka-lab-node
     - **browsers: chrome, firefox, edge, xboxone**
   - **visualstudio2022community**
 - shaka-test-mac1 ([M1 Mac mini][], running macOS 13)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - shaka-lab-browsers
   - shaka-lab-node
     - **browsers: chrome, safari**
 - shaka-test-mac2 ([Intel Mac mini (2018)][], running macOS 12)
   - shaka-lab-recommended-settings
   - shaka-lab-gateway-client
   - shaka-lab-browsers
   - shaka-lab-node
     - **browsers: firefox, edge**
 - gcloud-arm-runner-1 through gcloud-arm-runner5 ([Google Cloud ARM64 VMs][], running Ubuntu 22.04 LTS):
   - shaka-lab-recommended-settings
   - **shaka-lab-github-runner**
 - shaka-live-encoder-linux ([NUC 12 Enthusiast][], running Ubuntu 22.04 LTS)
   - **TODO(joeyparrish): Live encoder Linux details**
 - shaka-live-encoder-windows ([NUC 12 Enthusiast][], running Windows 11)
   - **TODO(joeyparrish): Live encoder Windows details**

[Topaz 2 NUC 12]: https://simplynuc.com/topaz-2/
[M1 Mac mini]: https://en.wikipedia.org/wiki/Mac_Mini#Apple_silicon_(2020%E2%80%93present)
[Intel Mac mini (2018)]: https://en.wikipedia.org/wiki/Mac_Mini#Space_gray_(2018)
[Google Cloud ARM64 VMs]: gcloud-arm-vms.md
[NUC 12 Enthusiast]: https://simplynuc.com/product/nuc12snki7-full/


## Device-specific prep

Some devices need BIOS/UEFI settings or other things changed before OS
installation.  Please check for your specific devices below.


### Topaz 2

Some BIOS settings need to be changed on the Topaz 2 hardware.

1. Press F2 during boot to enter device setup
2. Disable the splash screen
   - Boot > Full Screen Logo => Disabled
3. Disable net boot
   - Boot > Boot From Onboard LAN => Disabled
4. Set to boot when power is restored
   - Advanced > Chipset Configuration > Restore on AC/Power Loss => Power On


### NUC 12 Enthusiast

**TODO(joeyparrish): NUC 12 Enthusiast setup**

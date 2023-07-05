# Shaka Lab Packages


## Overview

This is all the software needed to replicate the private lab environment used to
build and test [Shaka Player](https://github.com/shaka-project/shaka-player),
[Shaka Packager](https://github.com/shaka-project/shaka-packager), and others.


## High-Level Goals

 - Speedy recovery after a disaster (disk corruption, exploding battery, etc)
 - Allow partners to replicate and contribute to our testing infrastructure
 - Replace aging, incomplete manual setup docs with version-controlled code


## Description

The Shaka Lab is composed of a
[Selenium grid](https://www.selenium.dev/documentation/grid/) and other
services running on multiple devices and operating systems.  Below are links to
dedicated docs on each package.

Setup involves installing relevant OS packages, editing configuration files,
and restarting services.  The available packages, config file locations, and
service commands vary by OS.

Package systems:
 - For Linux, [Debian](https://www.debian.org/)/[Ubuntu](https://ubuntu.com/)
   packages
 - For Windows, [Chocolatey](https://chocolatey.org/) packages
 - For macOS, [Homebrew](https://brew.sh/) formulae

Everything in this repo is licensed under [Apache license v2.0](LICENSE.txt).


## Package Guides

 - [Shaka Lab Recommended Settings](shaka-lab-recommended-settings/README.md#readme): Recommended OS settings for lab devices
 - [Shaka Lab Browsers](shaka-lab-browsers/README.md#readme): All major browsers, simplifies Selenium node setup
 - [Shaka Lab Hub](shaka-lab-hub/README.md#readme): Selenium grid hub (Linux only)
 - [Shaka Lab Node](shaka-lab-node/README.md#readme): Selenium grid nodes
 - [Shaka Lab Gateway](shaka-lab-gateway/README.md#readme): Lab gateway (DHCP, DNS, AD, routing)
 - [Shaka Lab Gateway Client](shaka-lab-gateway-client/README.md#readme): Central lab user login
 - [Shaka Lab Certs](shaka-lab-certs/README.md#readme): Automated certificates for HTTPS-based testing
 - [Shaka Lab GitHub Runner](shaka-lab-github-runner/README.md#readme): Self-hosted GitHub Actions runners


## Distribution Systems

Here you can find documentation for the various packge distribution systems
used, and their setup on GitHub.  You can read these to understand how packages
get distributed, or to help you debug issues with distribution.

If you want to deploy packages from a fork, you will need to read these and
follow the setup steps in each document.  Without those steps, the release
workflow will not work.

 - [Linux distribution](distribution/linux/README.md#readme)
 - [Windows distribution](distribution/windows/README.md#readme)
 - [macOS distribution](distribution/macos/README.md#readme)


## Consolidated Build Instructions

For consolidated instructions for our own lab build at Google, from OS
installation to a complete lab, see
[Shaka Lab Consolidated Build Instructions](consolidated-build/README.md#readme).
The details of your lab may vary.

# Shaka Lab Node for Windows

The Shaka Lab Node package provides Selenium grid nodes.
This is the Windows package.

For documentation on the package and configuration, or for links to other
platforms, see [the general docs](../README.md#readme).

**NOTE**: Browsers running in a Windows node **will not** be visible.

## Pre-requisites

 - Get Chocolatey: [https://docs.chocolatey.org/en-us/choco/setup](https://docs.chocolatey.org/en-us/choco/setup)

## Installation

```sh
choco source add -n=shaka-lab -s=https://shaka-lab-chocolatey-dot-shaka-player-demo.appspot.com/
choco install -y shaka-lab-node
```

## Updates

```sh
choco upgrade -y shaka-lab-node
```

## Running an Xbox One node

To run a Selenium node for Xbox One, you must also install Visual Studio.
If you don't have it, you can install it through chocolatey with:

```sh
choco install -y visualstudio2022community
```

## Configuration

The config file is at `c:\ProgramData\shaka-lab-node\node-config.yaml`.
See the [configuration section](../README.md#configuration) of the general doc.

## Restarting the service after editing the config

```sh
net stop shaka-lab-node
net start shaka-lab-node
```

## Tailing logs

```sh
powershell -command "Get-Content c:/ProgramData/shaka-lab-node/logs/shaka-lab-node-svc.err.log -Wait"
```

## Uninstallation

```sh
choco uninstall -y shaka-lab-node
```

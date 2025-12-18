# Embedd Peripheral Viewer

[![Visual Studio Marketplace](https://img.shields.io/visual-studio-marketplace/v/embedd-team.embedd-peripheral-viewer.svg)](https://marketplace.visualstudio.com/items?itemName=embedd-team.embedd-peripheral-viewer)
[![Open VSX](https://img.shields.io/badge/Open%20VSX-Published-green)](https://open-vsx.org/extension/embedd-team/embedd-peripheral-viewer)
[![VS Code](https://img.shields.io/badge/VS%20Code-Extension-blue?logo=visualstudiocode)](https://marketplace.visualstudio.com/items?itemName=embedd-team.embedd-peripheral-viewer)

## 🔀 Fork Manifest

This extension is a fork of the [peripheral-viewer](https://github.com/mcu-debug/peripheral-viewer).

It is developed and maintained as a component of [Embedd Project Manager](https://github.com/embeddteam/EmbeddedProjectManager.git) — a unified toolkit for embedded systems development in VS Code.

### Development Philosophy

While this fork evolves to meet the needs of Embedd Project Manager users, **it is not intended to diverge from upstream projects**.

All improvements, fixes, and enhancements introduced here are:
- Implemented with **upstream compatibility in mind**
- Submitted back to the original projects via **pull requests**
- Kept in sync through a **fast update and rebase cycle**

### Fast Iteration, Real Users

The primary goal of this fork is to enable:
- **Rapid iteration**
- **Early shipping**
- **Validation on real users**

This allows us to provide a **better and faster experience** for Embedd Project Manager users, while ensuring that the upstream ecosystem benefits from every improvement made here.

---

## ℹ️ About This Extension

Standalone SVD Viewer extension extracted from [cortex-debug](https://github.com/Marus/cortex-debug) but now work with any debugger that supports the Microsoft Debug Protocol

## Specifying SVD Files

The SVD Viewer extension uses [System View Description](http://www.keil.com/pack/doc/CMSIS/SVD/html/index.html) (SVD) files to display information about the selected part, including the Cortex Peripherals view.

Choose one of the following methods to specify your SVD file in your `launch.json` configuration(s):

### Use the CMSIS pack asset service

Set the `svdPath` configuration variable to a qualified pack reference in the form `<vendor>::<device family pack>@<version>` e.g.:

```json
{
    ...
    "svdPath": "NXP::K32L3A60_DFP@15.0.0"
    ...
}
```

If the pack supports multiple devices and/or processors, you will be prompted to select these. Alternatively, set them in your configuration using the optional `deviceName` and `processorName` variables:

```json
{
    ...
    "svdPath": "NXP::K32L3A60_DFP@15.0.0",
    "deviceName": "K32L3A60VPJ1A",
    "processorName": "cm4"
    ...
}
```

__TIP:__ The pack reference and device name can be automatically derived if you use the [Arm Device Manager extension in VS Code](https://marketplace.visualstudio.com/items?itemName=Arm.device-manager) using these commands:

```json
{
    ...
    "svdPath": "${command:device-manager.getDevicePack}",
    "deviceName": "${command:device-manager.getDeviceName}"
    ...
}
```

### Install a Cortex Debug Support Pack

Find a [Cortex Debug Support Pack](https://marketplace.visualstudio.com/search?term=Cortex-Debug%3A%20Device%20Support%20Pack&target=VSCode&category=All%20categories&sortBy=Relevance) for your device and install it. You can then specify just the `deviceName` variable in your launch configuration:

```json
{
    ...
    "deviceName": "STM32F439BI"
    ...
}
```

### Specify the path to your SVD file

You can obtain an SVD file from a [CMSIS pack](https://developer.arm.com/tools-and-software/embedded/cmsis/cmsis-packs) or from your device manufacturer. For example use [these instructions](https://community.st.com/s/question/0D50X00009XkWDkSAN/how-does-st-manage-svd-files) for ST devices.

Other vendors may ship SVD files when you install their software or device packs or you could write your own custom SVD file.

Once you have the SVD file, specify the location of it in your `launch.json` using the `svdPath` variable:

```json
{
    ...
    "svdPath": "${workspaceFolder}/STM32F103.svd"
    ...
}
```

### Extending MCU Peripheral Viewer

It is possible to extend the MCU Peripheral Viewer with your VSCode extension and provide peripherals information to the MCU Peripheral Viewer without passing an SVD file. In this method, `peripherals` variable passed to the debug launch configuration in `launch.json` file.

```json
{
    ...
    "peripherals": "command:myExtension.command.to.get.peripherals"
    ...
}
```

The `peripherals` variable will define the source to load the peripherals information. Peripherals could be loaded from VSCode command which is defined after `command:` prefix in `peripherals` variable. For more details about the implementation, please check the [Extending MCU Peripheral Viewer](./docs/extending-peripheral-viewer.md) document.

## Settings

All variable key names used to extract data from debug launch configurations can be modified. This allows variable name clashes to be avoided as well as the need to duplicate configuration entries.

The following list outlines the setting names and default values:

- `mcu-debug.peripheral-viewer.svdPathConfig` - Debug configuration key to use to get the SVD path (default `default`). If it is empty or set to `default`, the property `svdFile` is used for cortex-debug and `svdPath` for other debuggers.
- `mcu-debug.peripheral-viewer.deviceConfig` - Debug configuration key to use to get the device name (default: `deviceName`)
- `mcu-debug.peripheral-viewer.processorConfig` - Debug configuration key to use to get the processor name (default: `processorName`)

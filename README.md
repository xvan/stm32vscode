# STM32VScode

This is a fork of based on [STM32CubeF1](https://github.com/STMicroelectronics/STM32CubeF1)

This is a sample setup to build and debug stm32 projects in vscode.

Only some projects in path Projects/Examples/Bluepill have been configured.

Original projects were left as reference inside Projects/Examples/

Check Projects/BluePill/Examples/USB/CDC/CMakeLists.txt for the most complex project configuration.

Requirements
* OpenOCD
* An ARM-Eabi toolchain
* Cmake
* VsCode

Install the following Extensions in VScode:
* C/C++ Extension Pack (this inlcudes Cmake extensions)
* Command Variable (required to workaround path issue under windows)


Open the project root folder in VsCode

Configuration for sample blinky project:
```
	ctrl+shift+p -> cmake:select kit -> Unspecified
	ctrl+shift+p -> cmake:set build target -> GPIO_InfiniteLedToggling.elf
	ctrl+shift+p -> cmake:set Launch/Debug target -> GPIO_InfiniteLedToggling.elf
```

Build:
```
    ctrl+shift+p -> cmake:build
```

Launch:
```
	Run and Debug (left panel) -> OpenOCD GDB
```

Note: Cmake debug shortuct doesn't work with OpenOCD.

[Original STM32CubeF1 README](Original_README.md)

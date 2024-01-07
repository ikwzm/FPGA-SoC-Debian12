FPGA-SoC-Debian12
====================================================================================

Overview
------------------------------------------------------------------------------------

### Introduction

This Repository provides a Linux Boot Image(U-boot, Kernel, Debian12-Root-Fs) for FPGA-SoC.

### Note

**The Linux Kernel Image and Debian12 RootFS provided in this repository is not official.**

**I modified it to my liking. Please handle with care.**


### Features

* Hardware
  + ZYBO    : Xilinx Zynq-7000 ARM/FPGA SoC Trainer Board by Digilent
  + ZYBO-Z7 : Xilinx Zynq-7020 Development Board by Digilent
  + PYNQ-Z1 : Python Productive for Zynq by Digilent
  + DE0-Nano-SoC : Altera SoC FPGA Development Kit by Terasic
  + DE10-Nano    : Altera SoC FPGA Development Kit by Terasic
* U-Boot v2016.03 or v2017.11
  + Build U-Boot v2016.03 for ZYBO, PYNQ-Z1
  + Build U-Boot v2017.11 for ZYBO-Z7, DE0-Nano-SoC, DE10-Nano
  + Customized boot by uEnv.txt
  + Customized boot by boot.scr
  + Enable bootmenu
* Linux Kernel Version v6.1.xx
  + Available in both Xilinx-Zynq-7000 and Altera-SoC in a single image
  + Enable Device Tree Overlay
  + Enable FPGA Manager
  + Enable FPGA Bridge
  + Enable FPGA Reagion
  + Patch for issue #3(USB-HOST does not work with PYNQ-Z1)
* Debian12(bookworm) Root File System
  + Installed build-essential
  + Installed device-tree-compiler
  + Installed ruby ruby-msgpack ruby-serialport
  + Installed python python3 python3-numpy msgpack-rpc-python
  + Installed u-boot-tools
  + Installed Other package list -> [files/debian12-dpkg-list.txt](files/debian12-dpkg-list.txt)
* FPGA Device Drivers and Services
  + [dtbocfg    (Device Tree Blob Overlay Configuration File System)](https://github.com/ikwzm/dtbocfg)
  + [fclkcfg    (FPGA Clock Configuration Device Driver)](https://github.com/ikwzm/fclkcfg)
  + [udmabuf    (User space mappable DMA Buffer)](https://github.com/ikwzm/udmabuf)

Release
------------------------------------------------------------------------------------

| Release | Released   | Debian Version | Linux Kernel Version  | Release Tag |
|:--------|:-----------|:---------------|:----------------------|:------------|
| v4.0.0  | 2024-1-7   | Debian 12.4    | 6.1.70-armv7-fpga-1   | [v4.0.0](https://github.com/ikwzm/FPGA-SoC-Debian12/tree/v4.0.0)
| v1.1.0  | 2023-7-29  | Debian 12.1    | 6.1.42-armv7-fpga-1   | [v1.1.0](https://github.com/ikwzm/FPGA-SoC-Debian12/tree/v1.1.0)
| v1.0.0  | 2023-6-15  | Debian 12.0    | 6.1.33-armv7-fpga-1   | [v1.0.0](https://github.com/ikwzm/FPGA-SoC-Debian12/tree/v1.0.0)

Install (v4.0.0)
------------------------------------------------------------------------------------

* Install U-Boot and Linux to SD-Card
  + [ZYBO](doc/install/zynq-zybo.md)
  + [ZYBO-Z7](doc/install/zynq-zybo-z7.md)
  + [PYNQ-Z1](doc/install/zynq-pynqz1.md)
  + [DE0-Nano-SoC](doc/install/de0-nano-soc.md)
  + [DE10-Nano](doc/install/de10-nano.md)
* [Install Device Drivers and Services](doc/install/device-drivers.md)

FAQ
------------------------------------------------------------------------------------

* [Upgrade to Linux Kernel 6.1.70](doc/faq/upgrade-linux-kernel-6.1.70.md)

Build 
------------------------------------------------------------------------------------

* [Build U-boot for ZYBO](doc/build/u-boot-zynq-zybo.md)
* [Build U-boot for ZYBO-Z7](doc/build/u-boot-zynq-zybo-z7.md)
* [Build U-boot for PYNQ-Z1](doc/build/u-boot-zynq-pynqz1.md)
* [Build U-boot for DE0-Nano-SoC](doc/build/u-boot-de0-nano-soc.md)
* [Build U-boot for DE10-Nano](doc/build/u-boot-de10-nano.md)
* [Build Linux Kernel 6.1.70](https://github.com/ikwzm/FPGA-SoC-Debian12/blob/v4.0.0/doc/build/linux-kernel-6.1.70.md)
* [Build Debian12 RootFS](https://github.com/ikwzm/FPGA-SoC-Debian12/blob/v4.0.0/doc/build/debian12-rootfs.md)


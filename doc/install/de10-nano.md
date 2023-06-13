### DE10-Nano

#### Downlowd from github

**Note: Downloading the entire repository takes time, so download the source code from https://github.com/ikwzm/FPGA-SoC-Debian12/releases.**

```console
shell$ wget https://github.com/ikwzm/FPGA-SoC-Debian12/archive/refs/tags/v0.1.0.tar.gz
shell$ tar xfz v0.1.0.tar.gz
shell$ cd FPGA-SoC-Debian12-v0.1.0
```

#### File Description

 * target/de10-nano/
   + boot/
     - uEnv.txt                                                      : U-Boot environment variables for linux boot
     - devicetree-6.1.33-armv7-fpga-socfpga.dtb                      : Linux Device Tree Blob   
     - devicetree-6.1.33-armv7-fpga-socfpga.dts                      : Linux Device Tree Source
   + u-boot/
     - u-boot-spl.sfp                                                : Stage 1 Boot Loader(U-boot-spl)
     - u-boot.img                                                    : Stage 2 Boot Loader(U-boot)
 * files/
   + vmlinuz-6.1.33-armv7-fpga-1                                     : Linux Kernel Image
 * debian12-rootfs-vanilla.tgz.files/                                : Debian11 Root File System
   + x00 .. x08                                                      : (splited files)
 * debian/
   + linux-image-6.1.33-armv7-fpga_6.1.33-armv7-fpga-1_armhf.deb     : Linux Image Package
   + linux-headers-6.1.33-armv7-fpga_6.1.33-armv7-fpga-1_armhf.deb   : Linux Headers Package
   + dtbocfg-ctrl_0.0.5-1_all.deb                                    : dtbocfg Control Pakcage
   + dtbocfg-6.1.33-armv7-fpga_0.0.9-1_armhf.deb                     : dtbocfg Kernel Module
   + fclkcfg-6.1.33-armv7-fpga_1.7.2-1_armhf.deb                     : fclkcfg Kernel Module
   + u-dma-buf-6.1.33-armv7-fpga_3.2.5-0_armhf.deb                   : u-dma-buf Kernel Module
   + zptty-6.1.33-armv7-fpga_1.1.0-1_armhf.deb                       : zptty   Kernel Module

#### Format SD-Card

[./doc/install/format-disk-de0-nano-soc.md](format-disk-de0-nano-soc.md)

#### Write to SD-Card

````console
shell# export DISKDEV=/dev/sdc
shell# dd if=target/de10-nano/u-boot/u-boot-spl.sfp of=${DISKDEV}3 bs=64k seek=0
shell# dd if=target/de10-nano/u-boot/u-boot.img     of=${DISKDEV}3 bs=64k seek=4
shell# mount ${DISKDEV}1                                       /mnt/usb1
shell# mount ${DISKDEV}2                                       /mnt/usb2
shell# cp target/de10-nano/boot/*                              /mnt/usb1
shell# cp files/vmlinuz-6.1.33-armv7-fpga-1                    /mnt/usb1/vmlinuz-6.1.33-armv7-fpga
shell# cat debian11-rootfs-vanilla.tgz.files/* | tar xfz - -C  /mnt/usb2
shell# mkdir                                                   /mnt/usb2/home/fpga/debian
shell# cp debian/*                                             /mnt/usb2/home/fpga/debian
shell# umount                                                  /mnt/usb1
shell# umount                                                  /mnt/usb2
````

### Install Device Drivers and Services

[./doc/install/device-drivers.md](device-drivers.md)


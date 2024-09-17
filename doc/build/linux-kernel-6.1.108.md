### Build Linux Kernel 6.1.108-armv7-fpga

### Download FPGA-SoC-Linux-Kernel-6.1

```console
shell$ wget https://github.com/ikwzm/FPGA-SoC-Linux-Kernel-6.1/archive/refs/tags/6.1.108-armv7-fpga-1.tar.gz
shell$ tar xfz 6.1.108-armv7-fpga-1.tar.gz
```

### Setup parameters

```console
shell$ export LINUX_KERNEL_REPOSITORY=FPGA-SoC-Linux-Kernel-6.1-6.1.108-armv7-fpga-1
shell$ export LINUX_KERNEL_VERSION=6.1.108
shell$ export LINUX_KERNEL_RELEASE=$LINUX_KERNEL_VERSION-armv7-fpga
```


### Copy Linux Kernel Image to this repository

```console
shell$ cp $LINUX_KERNEL_REPOSITORY/vmlinuz-$LINUX_KERNEL_RELEASE-*      ./files
shell$ cp $LINUX_KERNEL_REPOSITORY/files/config-$LINUX_KERNEL_RELEASE-* ./files
```

### Copy Linux Image and Header Debian Packages to this repository

```console
shell$ cp $LINUX_KERNEL_REPOSITORY/linux-image-$LINUX_KERNEL_RELEASE_*.deb   ./debian
shell$ cp $LINUX_KERNEL_REPOSITORY/linux-headers-$LINUX_KERNEL_RELEASE_*.deb ./debian
```

### Copy devicetree to target/zybo-zynq/boot/

```console
shell$ export TARGET_NAME=zynq-zybo
shell$ export TARGET_DIR=target/zynq-zybo/boot
shell$ export TARGET_DTB=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dtb
shell$ export TARGET_DTS=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dts
shell$ install -d $TARGET_DIR
shell$ cp $LINUX_KERNEL_REPOSITORY/devicetrees/$LINUX_KERNEL_RELEASE-*/zynq-zybo.dtb $TARGET_DTB
shell$ dtc -I dtb -O dts -@ -o $TARGET_DTS $TARGET_DTB
```

or

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-6.1.108-armv7-fpga.sh -d target/zynq-zybo/boot -T -U -v zybo
```

### Copy devicetree to tareget/zybo-zynq-z7/boot/

```console
shell$ export TARGET_NAME=zynq-zybo-z7
shell$ export TARGET_DIR=target/zynq-zybo-z7/boot
shell$ export TARGET_DTB=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dtb
shell$ export TARGET_DTS=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dts
shell$ install -d $TARGET_DIR
shell$ cp $LINUX_KERNEL_REPOSITORY/devicetrees/$LINUX_KERNEL_RELEASE-*/zynq-zybo-z7.dtb $TARGET_DTB
shell$ dtc -I dtb -O dts -@ -o $TARGET_DTS $TARGET_DTB
```

or

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-6.1.108-armv7-fpga.sh -d target/zynq-zybo-z7/boot -T -U -v zybo-z7
```

### Copy devicetree to target/zybo-pynqz1/boot/

```console
shell$ export TARGET_NAME=zynq-pynqz1
shell$ export TARGET_DIR=target/zynq-pynqz1/boot
shell$ export TARGET_DTB=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dtb
shell$ export TARGET_DTS=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dts
shell$ install -d $TARGET_DIR
shell$ cp $LINUX_KERNEL_REPOSITORY/devicetrees/$LINUX_KERNEL_RELEASE-*/zynq-pynqz1.dtb $TARGET_DTB
shell$ dtc -I dtb -O dts -@ -o $TARGET_DTS $TARGET_DTB
```

or

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-6.1.108-armv7-fpga.sh -d target/zynq-pynqz1/boot -T -U -v pynq-z1
```

### Copy devicetree to target/de0-nano-soc/boot/

```console
shell$ export TARGET_NAME=socfpga
shell$ export TARGET_DIR=target/de0-nano-soc/boot
shell$ export TARGET_DTB=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dtb
shell$ export TARGET_DTS=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dts
shell$ install -d $TARGET_DIR
shell$ cp $LINUX_KERNEL_REPOSITORY/devicetrees/$LINUX_KERNEL_RELEASE-*/socfpga_cyclone5_de0_nano_soc.dtb $TARGET_DTB
shell$ dtc -I dtb -O dts -@ -o $TARGET_DTS $TARGET_DTB
```

or

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-6.1.108-armv7-fpga.sh -d target/de0-nano-soc/boot -T -U -v de0-nano-soc
```

### Copy devicetree to tareget/de10-nano/boot/

```console
shell$ export TARGET_NAME=socfpga
shell$ export TARGET_DIR=target/de10-nano/boot
shell$ export TARGET_DTB=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dtb
shell$ export TARGET_DTS=$TARGET_DIR/devicetree-$LINUX_KERNEL_RELEASE-$TARGET_NAME.dts
shell$ install -d $TARGET_DIR
shell$ cp $LINUX_KERNEL_REPOSITORY/devicetrees/$LINUX_KERNEL_RELEASE-*/socfpga_cyclone5_de0_nano_soc.dtb $TARGET_DTB
shell$ dtc -I dtb -O dts -@ -o $TARGET_DTS $TARGET_DTB
```

or

```console
shell$ bash $LINUX_KERNEL_REPOSITORY/scripts/install-linux-6.1.108-armv7-fpga.sh -d target/de10-nano/boot -T -U -v de10-nano
```


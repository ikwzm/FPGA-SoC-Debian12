### Upgrade Linux Kernel to 6.1.47

#### Boot ZYBO/ZYBO-Z7/PYNQ-Z1/DE0-Nano-SoC/DE10-Nano and login fpga or root user

fpga'password is "fpga".

```console
debian-fpga login: fpga
Password:
fpga@debian-fpga:~$
```

root'password is "admin".

```console
debian-fpga login: root
Password:
root@debian-fpga:~#
```

#### Download Linux Kernel 6.1.47

```console
root@debian-fpga:~# wget https://github.com/ikwzm/FPGA-SoC-Linux-Kernel-6.1/archive/refs/tags/6.1.47-armv7-fpga-1.tar.gz
--2023-08-28 13:07:55--  https://github.com/ikwzm/FPGA-SoC-Linux-Kernel-6.1/archive/refs/tags/6.1.47-armv7-fpga-1.tar.gz
Resolving github.com (github.com)... 20.27.177.113
Connecting to github.com (github.com)|20.27.177.113|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://codeload.github.com/ikwzm/FPGA-SoC-Linux-Kernel-6.1/tar.gz/refs/tags/6.1.47-armv7-fpga-1 [following]
--2023-08-28 13:07:56--  https://codeload.github.com/ikwzm/FPGA-SoC-Linux-Kernel-6.1/tar.gz/refs/tags/6.1.47-armv7-fpga-1
Resolving codeload.github.com (codeload.github.com)... 20.27.177.114
Connecting to codeload.github.com (codeload.github.com)|20.27.177.114|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [application/x-gzip]
Saving to: ‘6.1.47-armv7-fpga-1.tar.gz’

6.1.47-armv7-fpga-1     [               <=>  ]  23.91M  6.50MB/s    in 3.8s

2023-08-28 13:08:00 (6.36 MB/s) - ‘6.1.47-armv7-fpga-1.tar.gz’ saved [25073087]
root@debian-fpga:~# tar xfz 6.1.47-armv7-fpga-1.tar.gz
root@debian-fpga:~# cd FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1/
```

#### Install Linux Kernel Image and Device Tree to Boot Partition (Example with ZYBO-Z7)

```console
root@debian-fpga:~/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1# ./scripts/install-linux-6.1.47-armv7-fpga.sh -d /mnt/boot -v zybo-z7
# SCRIPT NAME     =  ./scripts/install-linux-6.1.47-armv7-fpga.sh
# SCRIPT VERSION  =  0.1
# KERNEL_RELEASE  =  6.1.47-armv7-fpga
# BUILD_VERSION   =  1
# TARGET          =  zynq_zybo_z7
# TARGET_DIRECTRY =  /mnt/boot
install -d /mnt/boot
cp /root/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1/vmlinuz-6.1.47-armv7-fpga-1 /mnt/boot/vmlinuz-6.1.47-armv7-fpga
# do_install_dtb(zynq_zybo_z7)
cp /root/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1/devicetrees/6.1.47-armv7-fpga-1/zynq-zybo-z7.dtb /mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dtb
dtc -I dtb -O dts --symbols -o /mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts /mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dtb
/mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts: Warning (unit_address_vs_reg): /reserved-memory/zynq-dma-unusable-area: node has a reg or ranges property, but no unit name
/mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts: Warning (unit_address_vs_reg): /phy0: node has a reg or ranges property, but no unit name
/mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts: Warning (simple_bus_reg): /axi/fpga-region0: missing or empty reg/ranges property
/mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts: Warning (interrupt_provider): /axi/gpio@e000a000: Missing #address-cells in interrupt provider
/mnt/boot/devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dts: Warning (interrupt_provider): /axi/interrupt-controller@f8f01000: Missing #address-cells in interrupt provider
```

#### Update uEnv.txt on Boot Partition (Example with ZYBO-Z7)

##### Backup uEnv.txt

```console
root@debian-fpga:~/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1# cp /mnt/boot/uEnv.txt /mnt/boot/uEnv.txt.old
```

##### Change uEnv.txt

```console
root@debian-fpga:~/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1# sed -E 's/^linux_kernel_image=.*/linux_kernel_image=vmlinuz-6.1.47-armv7-fpga/ ; s/^linux_fdt_image=.*/linux_fdt_image=devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dtb/' /mnt/boot/uEnv.txt.old > /mnt/boot/uEnv.txt
```

##### Check uEnv.txt

```console
root@debian-fpga:~/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1# diff -u /mnt/boot/uEnv.txt.old /mnt/boot/uEnv.txt
--- /mnt/boot/uEnv.txt.old      2023-08-28 13:23:12.000000000 +0900
+++ /mnt/boot/uEnv.txt  2023-08-28 13:53:54.000000000 +0900
@@ -3,8 +3,8 @@
 #  * linux_kernel_image : Linux Kernel Image File Name
 #  * linux_fdt_image    : Linux Device Tree Blob File Name
 ########################################################################
-linux_kernel_image=vmlinuz-6.1.42-armv7-fpga
-linux_fdt_image=devicetree-6.1.42-armv7-fpga-zynq-zybo-z7.dtb
+linux_kernel_image=vmlinuz-6.1.47-armv7-fpga
+linux_fdt_image=devicetree-6.1.47-armv7-fpga-zynq-zybo-z7.dtb

 ########################################################################
 # Linux Boot Argments
```

#### Install Linux Image Debian Package

```console
root@debian-fpga:~/FPGA-SoC-Linux-Kernel-6.1-6.1.47-armv7-fpga-1# dpkg -i linux-image-6.1.47-armv7-fpga_6.1.47-armv7-fpga-1_armhf.deb
Selecting previously unselected package linux-image-6.1.47-armv7-fpga.
(Reading database ... 61538 files and directories currently installed.)
Preparing to unpack linux-image-6.1.47-armv7-fpga_6.1.47-armv7-fpga-1_armhf.deb ...
Unpacking linux-image-6.1.47-armv7-fpga (6.1.47-armv7-fpga-1) ...
Setting up linux-image-6.1.47-armv7-fpga (6.1.47-armv7-fpga-1) ...
```


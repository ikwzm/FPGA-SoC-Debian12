### Build Debian12 RootFS

#### Prepare Linux Kernel Image Debian Package

[./doc/build/linux-kernel-6.1.108.md](linux-kernel-6.1.108.md)

#### Setup parameters 

```console
shell$ sudo apt install qemu-user-static debootstrap binfmt-support
shell$ export targetdir=debian12-rootfs
shell$ export distro=bookworm
```

#### Build Debian RootFS first-step in $targetdir(=debian12-rootfs)

```console
shell$ mkdir                                                                        $PWD/$targetdir
shell$ sudo chown root                                                              $PWD/$targetdir
shell$ sudo debootstrap --arch=armhf --foreign $distro                              $PWD/$targetdir
shell$ sudo cp /usr/bin/qemu-arm-static                                             $PWD/$targetdir/usr/bin
shell$ sudo cp /etc/resolv.conf                                                     $PWD/$targetdir/etc
shell$ sudo cp scripts/build-debian12-rootfs-with-qemu.sh                           $PWD/$targetdir
shell$ sudo cp debian/linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb $PWD/$targetdir
```

If you get an error like the following, debootstrap does not yet support bookworm in your environment.

```console
shell$ sudo debootstrap --arch=armhf --foreign $distro                              $PWD/$targetdir
E: No such script: /usr/share/debootstrap/scripts/bookworm
```

Please install a debootstrap that does not support bookworm as follows

```console
shell$ sudo dpkg -i debian/debootstrap_1.0.128+nmu2_all.deb
```

#### Build Debian RootFS second-step with QEMU

##### Change Root to debian12-rootfs

```console
shell$ sudo chroot $PWD/$targetdir
```

There are two ways

1. run build-debian12-rootfs-with-qemu.sh (easy)
2. run this chapter step-by-step (annoying)

##### Run debootstrap second stage

```console
debian12-rootfs# distro=bookworm
debian12-rootfs# export LANG=C
debian12-rootfs# /debootstrap/debootstrap --second-stage
```

##### Setup APT

```console
debian12-rootfs# cat <<EOT > /etc/apt/sources.list
deb     http://ftp.jp.debian.org/debian  bookworm           main contrib non-free non-free-firmware
deb-src http://ftp.jp.debian.org/debian  bookworm           main contrib non-free non-free-firmware
deb     http://ftp.jp.debian.org/debian  bookworm-updates   main contrib non-free non-free-firmware
deb-src http://ftp.jp.debian.org/debian  bookworm-updates   main contrib non-free non-free-firmware
deb     http://security.debian.org       bookworm-security  main contrib non-free non-free-firmware
deb-src http://security.debian.org       bookworm-security  main contrib non-free non-free-firmware
EOT
```

```console
debian12-rootfs# cat <<EOT > /etc/apt/apt.conf.d/71-no-recommends
APT::Install-Recommends "0";
APT::Install-Suggests   "0";
EOT
```

```console
debian12-rootfs# apt update -y
debian12-rootfs# apt upgrade -y
```

##### Install applications

```console
debian12-rootfs# apt install -y locales dialog
debian12-rootfs# dpkg-reconfigure locales
debian12-rootfs# apt install -y net-tools openssh-server ntpdate resolvconf sudo less hwinfo ntp tcsh zsh file
```

please select "97. en_US.UTF-8 UTF-8" and "2. C.UTF-8"

##### Setup hostname

```console
debian12-rootfs# echo debian-fpga > /etc/hostname
```

##### Setup root password

```console
debian12-rootfs# passwd
```

This time, we set the "admin" at the root' password.

To be able to login as root from Zynq serial port.

```console
debian12-rootfs# cat <<EOT >> /etc/securetty
# Seral Port for Xilinx Zynq
ttyPS0
EOT
```

##### Add a new guest user

```console
debian12-rootfs# adduser fpga
```

This time, we set the "fpga" at the fpga'password.

```console
debian12-rootfs# apt install -y sudo
debian12-rootfs# echo "fpga ALL=(ALL:ALL) ALL" > /etc/sudoers.d/fpga
```

##### Setup sshd config

```console
debian12-rootfs# apt install -y ssh
debian12-rootfs# sed -i -e 's/#PasswordAuthentication/PasswordAuthentication/g' /etc/ssh/sshd_config
```

##### Setup Time Zone

```console
debian12-rootfs# dpkg-reconfigure tzdata
```

or if noninteractive set to Asia/Tokyo

```console
debian12-rootfs# echo "Asia/Tokyo" > /etc/timezone
debian12-rootfs# dpkg-reconfigure -f noninteractive tzdata
```


##### Setup fstab

```console
debian12-rootfs# cat <<EOT > /etc/fstab
/dev/mmcblk0p1	/mnt/boot	auto		defaults	0	0
none		/config		configfs	defaults	0	0
EOT
````

##### Setup Network

```console
debian10-rootfs# apt install -y ifupdown
debian10-rootfs# cat <<EOT > /etc/network/interfaces.d/end0
allow-hotplug end0
iface end0 inet dhcp
EOT
````

##### Setup /lib/firmware

```console
debian12-rootfs# mkdir /lib/firmware
```

##### Install Wireless tools and firmware

```console
debian12-rootfs# apt install -y wireless-tools
debian12-rootfs# apt install -y wpasupplicant
debian12-rootfs# apt install -y firmware-realtek
debian12-rootfs# apt install -y firmware-ralink
```

##### Install Development applications

```console
debian12-rootfs# apt install -y build-essential
debian12-rootfs# apt install -y git git-lfs
debian12-rootfs# apt install -y u-boot-tools device-tree-compiler
debian12-rootfs# apt install -y libssl-dev
debian12-rootfs# apt install -y socat
debian12-rootfs# apt install -y ruby rake ruby-msgpack ruby-serialport 
debian12-rootfs# apt install -y python3 python3-dev python3-setuptools python3-wheel python3-pip python3-numpy
debian12-rootfs# apt install -y flex bison pkg-config
debian12-rootfs# apt install -y file dosfstools
```

##### Install Other applications

```console
debian12-rootfs# apt install -y samba
debian12-rootfs# apt install -y avahi-daemon
```

##### Install haveged for Linux Kernel 4.19

```console
debian12-rootfs# apt install -y haveged
```

##### Install Linux Modules

```console
debian12-rootfs# mkdir /mnt/boot
debian12-rootfs# dpkg -i linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb
```

##### Clean APT Cache

```console
debian12-rootfs# apt clean
```

##### Create Debian Package List

```console
debian12-rootfs# dpkg -l > dpkg-list.txt
```

##### Finish

```console
debian12-rootfs# exit
shell$ sudo rm -f  $PWD/$targetdir/usr/bin/qemu-arm-static
shell$ sudo rm -f  $PWD/$targetdir/build-debian12-rootfs-with-qemu.sh
shell$ sudo rm -f  $PWD/$targetdir/linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb
shell$ sudo mv     $PWD/$targetdir/dpkg-list.txt files/debian12-dpkg-list.txt
```

##### Clean User Directory on pip build

```console
shell$ sudo rm -rf $PWD/$targetdir/home/$USERNAME
```

#### Build debian12-rootfs-vanilla.tgz

```console
shell$ cd $PWD/$targetdir
shell$ sudo tar cfz ../debian12-rootfs-vanilla.tgz *
shell$ cd ..
```

#### Build debian12-rootfs-vanilla.tgz.files

```console
shell$ mkdir debian12-rootfs-vanilla.tgz.files
shell$ cd    debian12-rootfs-vanilla.tgz.files
shell$ split -d --bytes=40M ../debian12-rootfs-vanilla.tgz
shell$ cd ..
```

### Install Device Drivers and Services

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

#### Install Kernel Image Package

Since linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb is already pre-installed in debian12-rootfs-vanilla, this The process can be omitted.

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb
Selecting previously unselected package linux-image-6.1.108-armv7-fpga.
(Reading database ... 79019 files and directories currently installed.)
Preparing to unpack linux-image-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb ...
Unpacking linux-image-6.1.108-armv7-fpga (6.1.108-armv7-fpga-1) ...
Setting up linux-image-6.1.108-armv7-fpga (6.1.108-armv7-fpga-1) ...
```

#### Install Kernel Header Packages

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i linux-headers-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb
Selecting previously unselected package linux-headers-6.1.108-armv7-fpga.
(Reading database ... 79407 files and directories currently installed.)
Preparing to unpack linux-headers-6.1.108-armv7-fpga_6.1.108-armv7-fpga-1_armhf.deb ...
Unpacking linux-headers-6.1.108-armv7-fpga (6.1.108-armv7-fpga-1) ...
Setting up linux-headers-6.1.108-armv7-fpga (6.1.108-armv7-fpga-1) ...
make: Entering directory '/usr/src/linux-headers-6.1.108-armv7-fpga'
  SYNC    include/config/auto.conf.cmd
  HOSTCC  scripts/basic/fixdep
  HOSTCC  scripts/kconfig/conf.o
  HOSTCC  scripts/kconfig/confdata.o
  HOSTCC  scripts/kconfig/expr.o
  LEX     scripts/kconfig/lexer.lex.c
  YACC    scripts/kconfig/parser.tab.[ch]
  HOSTCC  scripts/kconfig/lexer.lex.o
  HOSTCC  scripts/kconfig/menu.o
  HOSTCC  scripts/kconfig/parser.tab.o
  HOSTCC  scripts/kconfig/preprocess.o
  HOSTCC  scripts/kconfig/symbol.o
  HOSTCC  scripts/kconfig/util.o
  HOSTLD  scripts/kconfig/conf
*
* Restart config...
*
*
* Kernel Features
*
Symmetric Multi-Processing (SMP) [Y/n/?] y
  Allow booting SMP kernel on uniprocessor systems (SMP_ON_UP) [Y/n/?] y
Support cpu topology definition (ARM_CPU_TOPOLOGY) [Y/n/?] y
  Multi-core scheduler support (SCHED_MC) [Y/n/?] y
  SMT scheduler support (SCHED_SMT) [Y/n/?] y
Architected timer support (HAVE_ARM_ARCH_TIMER) [N/y/?] n
Multi-Cluster Power Management (MCPM) [N/y/?] n
big.LITTLE support (Experimental) (BIG_LITTLE) [N/y/?] n
Memory split
> 1. 3G/1G user/kernel split (VMSPLIT_3G)
  2. 3G/1G user/kernel split (for full 1G low memory) (VMSPLIT_3G_OPT)
  3. 2G/2G user/kernel split (VMSPLIT_2G)
  4. 1G/3G user/kernel split (VMSPLIT_1G)
choice[1-4?]: 1
Maximum number of CPUs (2-32) (NR_CPUS) [2] 2
Support for hot-pluggable CPUs (HOTPLUG_CPU) [Y/?] y
Support for the ARM Power State Coordination Interface (PSCI) (ARM_PSCI) [N/y/?] n
Timer frequency
> 1. 100 Hz (HZ_100)
  2. 200 Hz (HZ_200)
  3. 250 Hz (HZ_250)
  4. 300 Hz (HZ_300)
  5. 500 Hz (HZ_500)
  6. 1000 Hz (HZ_1000)
choice[1-6?]: 1
Compile the kernel in Thumb-2 mode (THUMB2_KERNEL) [N/y/?] n
Runtime patch udiv/sdiv instructions into __aeabi_{u}idiv() (ARM_PATCH_IDIV) [Y/n/?] y
Use the ARM EABI to compile the kernel (AEABI) [Y/?] y
  Allow old ABI binaries to run with this kernel (EXPERIMENTAL) (OABI_COMPAT) [N/y/?] n
High Memory Support (HIGHMEM) [Y/n/?] y
  Allocate 2nd-level pagetables from highmem (HIGHPTE) [Y/n/?] y
Enable use of CPU domains to implement privileged no-access (CPU_SW_DOMAIN_PAN) [Y/n/?] y
Use PLTs to allow module memory to spill over into vmalloc area (ARM_MODULE_PLTS) [N/y/?] n
Maximum zone order (ARCH_FORCE_MAX_ORDER) [11] 11
Use kernel mem{cpy,set}() for {copy_to,clear}_user() (UACCESS_WITH_MEMCPY) [N/y/?] n
Enable paravirtualization code (PARAVIRT) [N/y/?] n
Paravirtual steal time accounting (PARAVIRT_TIME_ACCOUNTING) [N/y/?] n
Xen guest support on ARM (XEN) [N/y/?] n
Use a unique stack canary value for each task (STACKPROTECTOR_PER_TASK) [Y/n/?] (NEW)
*
* Memory initialization
*
Initialize kernel stack variables at function entry
> 1. no automatic stack variable initialization (weakest) (INIT_STACK_NONE)
  2. pattern-init everything (strongest) (INIT_STACK_ALL_PATTERN) (NEW)
  3. zero-init everything (strongest and safest) (INIT_STACK_ALL_ZERO) (NEW)
choice[1-3?]:
Enable heap memory zeroing on allocation by default (INIT_ON_ALLOC_DEFAULT_ON) [N/y/?] n
Enable heap memory zeroing on free by default (INIT_ON_FREE_DEFAULT_ON) [N/y/?] n
Enable register zeroing on function exit (ZERO_CALL_USED_REGS) [N/y/?] (NEW)
  HOSTCC  scripts/dtc/dtc.o
  HOSTCC  scripts/dtc/flattree.o
  HOSTCC  scripts/dtc/fstree.o
  HOSTCC  scripts/dtc/data.o
  HOSTCC  scripts/dtc/livetree.o
  HOSTCC  scripts/dtc/treesource.o
  HOSTCC  scripts/dtc/srcpos.o
  HOSTCC  scripts/dtc/checks.o
  HOSTCC  scripts/dtc/util.o
  HOSTCC  scripts/dtc/dtc-lexer.lex.o
  HOSTCC  scripts/dtc/dtc-parser.tab.o
  HOSTLD  scripts/dtc/dtc
  HOSTCC  scripts/dtc/libfdt/fdt.o
  HOSTCC  scripts/dtc/libfdt/fdt_ro.o
  HOSTCC  scripts/dtc/libfdt/fdt_wip.o
  HOSTCC  scripts/dtc/libfdt/fdt_sw.o
  HOSTCC  scripts/dtc/libfdt/fdt_rw.o
  HOSTCC  scripts/dtc/libfdt/fdt_strerror.o
  HOSTCC  scripts/dtc/libfdt/fdt_empty_tree.o
  HOSTCC  scripts/dtc/libfdt/fdt_addresses.o
  HOSTCC  scripts/dtc/libfdt/fdt_overlay.o
  HOSTCC  scripts/dtc/fdtoverlay.o
  HOSTLD  scripts/dtc/fdtoverlay
  HOSTCC  scripts/genksyms/genksyms.o
  HOSTCC  scripts/genksyms/parse.tab.o
  HOSTCC  scripts/genksyms/lex.lex.o
  HOSTLD  scripts/genksyms/genksyms
  HOSTCC  scripts/kallsyms
  HOSTCC  scripts/sorttable
  HOSTCC  scripts/asn1_compiler
  CC      scripts/mod/empty.o
  HOSTCC  scripts/mod/mk_elfconfig
  MKELF   scripts/mod/elfconfig.h
  HOSTCC  scripts/mod/modpost.o
  CC      scripts/mod/devicetable-offsets.s
  HOSTCC  scripts/mod/file2alias.o
  HOSTCC  scripts/mod/sumversion.o
  HOSTLD  scripts/mod/modpost
make: Leaving directory '/usr/src/linux-headers-6.1.108-armv7-fpga'
```


#### Install dtbocfg kernel module package

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i dtbocfg-6.1.108-armv7-fpga_0.1.0-1_armhf.deb
Selecting previously unselected package dtbocfg-6.1.108-armv7-fpga.
(Reading database ... 95705 files and directories currently installed.)
Preparing to unpack dtbocfg-6.1.108-armv7-fpga_0.1.0-1_armhf.deb ...
Unpacking dtbocfg-6.1.108-armv7-fpga (0.1.0-1) ...
Setting up dtbocfg-6.1.108-armv7-fpga (0.1.0-1) ...
```

#### Install fclkcfg kernel module package

```console
fpga@debian-fpga:~/debian$ dpkg -i fclkcfg-6.1.108-armv7-fpga_1.7.3-1_armhf.deb
Selecting previously unselected package fclkcfg-6.1.108-armv7-fpga.
(Reading database ... 95711 files and directories currently installed.)
Preparing to unpack fclkcfg-6.1.108-armv7-fpga_1.7.3-1_armhf.deb ...
Unpacking fclkcfg-6.1.108-armv7-fpga (1.7.3-1) ...
Setting up fclkcfg-6.1.108-armv7-fpga (1.7.3-1) ...
```

#### Install u-dma-buf kernel module package

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i u-dma-buf-6.1.108-armv7-fpga_4.6.1-0_armhf.deb
Selecting previously unselected package u-dma-buf-6.1.108-armv7-fpga.
(Reading database ... 95716 files and directories currently installed.)
Preparing to unpack u-dma-buf-6.1.108-armv7-fpga_4.6.1-0_armhf.deb ...
Unpacking u-dma-buf-6.1.108-armv7-fpga (4.6.1-0) ...
Setting up u-dma-buf-6.1.108-armv7-fpga (4.6.1-0) ...
```

#### Install zynq-afi kernel module package

This debian package only installs ZYNQ(ZYBO/ZYBO-Z7/PYNQ-Z1).

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i zynq-afi-6.1.108-armv7-fpga_0.0.1-0_armhf.deb
Selecting previously unselected package zynq-afi-6.1.108-armv7-fpga.
(Reading database ... 95722 files and directories currently installed.)
Preparing to unpack zynq-afi-6.1.108-armv7-fpga_0.0.1-0_armhf.deb ...
Unpacking zynq-afi-6.1.108-armv7-fpga (0.0.1-0) ...
Setting up zynq-afi-6.1.108-armv7-fpga (0.0.1-0) ...
```

#### Install dtbocfg control package

```console
fpga@debian-fpga:~/debian$ sudo dpkg -i dtbocfg-ctrl_0.0.5-1_all.deb
Selecting previously unselected package dtbocfg-ctrl.
(Reading database ... 95722 files and directories currently installed.)
Preparing to unpack dtbocfg-ctrl_0.0.5-1_all.deb ...
Unpacking dtbocfg-ctrl (0.0.5-1) ...
Setting up dtbocfg-ctrl (0.0.5-1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/device-tree-overlay.service → /etc/systemd/system/device-tree-overlay.service.
[ 1037.524320] dtbocfg: 0.1.0
[ 1037.527119] dtbocfg: OK
```

#### Check Installed Device Drivers and Services Package

```console
fpga@debian-fpga:~$ sudo lsmod
Module                  Size  Used by
dtbocfg                16384  0
```

```console
fpga@debian-fpga:~/debian$ sudo systemctl status device-tree-overlay.service --no-pager -l
● device-tree-overlay.service - Device Tree Overlay Service.
     Loaded: loaded (/etc/systemd/system/device-tree-overlay.service; enabled; preset: enabled)
     Active: active (exited) since Tue 2024-09-17 07:03:02 JST; 8min ago
    Process: 3004 ExecStart=/sbin/modprobe dtbocfg (code=exited, status=0/SUCCESS)
   Main PID: 3004 (code=exited, status=0/SUCCESS)
        CPU: 29ms

Sep 17 07:03:02 debian-fpga systemd[1]: Starting device-tree-overlay.service - Device Tree Overlay Service....
Sep 17 07:03:02 debian-fpga systemd[1]: Finished device-tree-overlay.service - Device Tree Overlay Service..
```


# Notes on using Yoe on the Xilinx ZCU102

[up](README.md)

[BSP Layer documentation](meta-xilinx/meta-xilinx-bsp/README.building.md)

## Building/installing an image

1. `git clone git://github.com/YoeDistro/yoe-distro.git`
1. `cd yoe-distro`
1. `. zcu102-zynqmp-envsetup.sh`
1. `yoe_setup`
1. add following to conf/local.conf
IMAGE\_BOOT\_FILES\_append = " boot.bin"
PREFERRED\_PROVIDER\_virtual/pmu-firmware = "pmu-firmware"
PREFERRED\_PROVIDER\_virtual/boot-bin = "xilinx-bootbin"
PREFERRED\_PROVIDER\_virtual/dtb = "device-tree"
PREFERRED\_PROVIDER\_qemu-native = "qemu-xilinx-native"
PREFERRED\_PROVIDER\_qemu-helper-native = "qemu-helper-native"
IMAGE\_INSTALL\_remove = " qemu"
1. `bitbake petalinux-image-minimal`
1. insert SD card
1. `lsblk` (note sd card device, and substitute for /dev/sdX below)
1. `yoe_install_image /dev/sdX petalinux-image-minimal`
1. optional: configure console for serial port (see below)
1. `sudo eject /dev/sdX`

*core-image-minimal also worked, but yoe-simple-image would not boot up and gets stuck in kernel *

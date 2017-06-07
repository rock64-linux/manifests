Rock64 readme (Source Code: https://github.com/rock64-linux)

Get the source code:
	repo init -u https://github.com/rock64-linux/manifests
	repo sync

Download the prebuilt Debian rootfs image from:
	https://drive.google.com/folderview?id=0BwAJtUrQohwXdGRVYTAwdlJDOUU&usp=sharing
	Download rootfs-debian-20170504-beta-5 and extract "linaro-rootfs.img" file to current working directory	
	
Building kernel:
	cd kernel
	make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- rockchip_linux_defconfig
	make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- -j4

Building u-boot:
	cd u-boot
	CROSS_COMPILE=aarch64-linux-gnu- make rock64_defconfig all

Buiding kernel and u-boot image:
	build/mk-kernel.sh rock64
	build/mk-uboot.sh rock64
	
Building one system image:
	build/mk-image.sh -c rock64 -t system -s 4000 -r linaro-rootfs.img
	
Update image: 
	sdcard: build/flash_tool.sh -c rock64  -d /dev/sdb -p system  -i  out/system.img 
	sync
	
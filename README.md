# UART free Zyxel ex5601 OpenWrt to OEM . and OpenWrt ubootmod to OpenWrt stock Converter
UART-free conversion between OpenWrt ubootmod, OpenWrt stock layout, and OEM Zyxel firmware for EX5601-T0 /T-56.
 If you have Openwrt ubootmod installed on EX5601-T0 / T-56 router
 With this tool you can 
 1) Convert Openwrt ubootmod to Openwrt stock layout
 2) Convert Openwrt to OEM zyxel firmware

> [!WARNING]
> Power loss during flash can brick the device.
> Keep backups of important MTD partitions before flash

## Quick Install
Make sure internet connection is working on router, then use these commands, head to LUCI at port 8080 to finish installation 
```bash
cd /tmp
wget \
https://raw.githubusercontent.com/majad00/ex5601_openwrt_loader/main/tools/openwrt_chroot_rootfs.tar.gz \
https://raw.githubusercontent.com/majad00/ex5601_openwrt_loader/main/tools/loader.sh
chmod +x loader.sh ; ./loader.sh
```

## Offline Install 
Download the installation bundle from /tools ( two files)
1) Miniroot Archive (openwrt_chroot_rootfs.tar.gz)
2) Main script (loader.sh ) 

Copy both files to the router's /tmp dir using WinSCP or the SCP:

```bash
scp openwrt_chroot_rootfs.tar.gz loader.sh root@192.168.1.1:/tmp/
```
Alternatively, you can copy files to a USB drive and then use the USB drive 

```bash
mount /dev/sda1 /mnt/usb
cp /mnt/usb/openwrt_chroot_rootfs.tar.gz /tmp

```
 Starting

(Assuming you have root access on SSH)
```bash
chmod +x /tmp/loader.sh
/tmp/loader.sh
```

Once the script completes, LUCI web server will be running in your RAM at port 8080. 
Flash Openwrt from LUCI menu ... System > Install matrix > and select to flash Openwrt-stock layout or U-boot layout.
### Router reboot at the end , usually it take 10 to 15 seconds for full installation.

## Expert's Guide
This bundle provides a safe way to install OpenWrt on the Zyxel EX5601-T0 router directly from the OEM firmware flashing inactive partition, how we do that.

- **`loader.sh`** - A script that creates a Matrix/OpenWrt chroot environment on your running OEM firmware, similar to the second phase of sysupgrade. Instead of immediately flashing, it sets up additional services and the LuCI web interface to help you activate OpenWrt from within the OEM firmware at port 8080.

- **`openwrt_chroot_rootfs.tar.gz`** - OpenWrt rootfs with minimal services enabled.

> **Update**: With the latest update, now it is also possible to flash OpenWrt U-Boot layout safely.

---

### How build from source

Project B is part of main project and based on the source from 
https://github.com/majad00/ex5601_openwrt_loader



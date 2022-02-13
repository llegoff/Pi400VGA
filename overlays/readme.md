https://github.com/Cpasjuste/rpi-dpidac
https://www.higithub.com/rtomasa/repo/rpi-dpidac

overlays for recalbox 8
recalbox 8 use driver rpi-dpidac

vc4-vga666.dtbo-> /boot/overlays/vc4-vga666.dtbo

rpi-dpidac.ko -> driver folder

   /lib/modules/5.10.79-v7l/extra/rpi-dpidac.ko

   /overlay/lower/lib/modules/5.10.79-v7l/extra/rpi-dpidac.ko


### patch recalbox 8

copy rpi-dpidac.ko and vc4-vga666.dtbo in fat32 partition in overlays folder

ssh recalbox

    cd /
    mount -o remount,rw /
    cd /lib/modules/5.10.79-v71/extra/
    rm rpi-dpidac.ko
    cp /boot/overlays/rpi-dpidac.ko rpi-dpidac.ko
    chmod 644 rpi-dpidac.ko
    rm /boot/overlays/rpi-dpidac.ko

reboot


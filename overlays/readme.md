https://github.com/Cpasjuste/rpi-dpidac

https://www.higithub.com/rtomasa/repo/rpi-dpidac

https://gitlab.com/recalbox/recalbox/-/tree/master/projects/recalbox-rgb-dual

overlays for recalbox 8
recalbox 8 use driver rpi-dpidac

vc4-vga666.dtbo-> /boot/overlays/vc4-vga666.dtbo

rpi-dpidac.ko -> driver folder

   /lib/modules/5.10.79-v7l/extra/rpi-dpidac.ko

   /overlay/lower/lib/modules/5.10.79-v7l/extra/rpi-dpidac.ko


### patch recalbox 8

copy recalboxrgbdual.ko and recalboxrgbdual-thirdparty.dtbo in the overlays folder of the fat32 partition

ssh recalbox

    cd /
    mount -o remount,rw /
    cd /lib/modules/5.10.83-v7l/extra/
    rm rpi-dpidac.ko
    cp /boot/overlays/recalboxrgbdual.ko recalboxrgbdual.ko
    chmod 644 rpi-dpidac.ko
    
reboot


https://github.com/Cpasjuste/rpi-dpidac

https://www.higithub.com/rtomasa/repo/rpi-dpidac

https://gitlab.com/recalbox/recalbox/-/tree/master/projects/recalbox-rgb-dual

overlays for recalbox 8

recalbox 8 use driver rpi-dpidac


### patch recalbox 8

copy recalboxrgbdual.ko and recalboxrgbdual-thirdparty.dtbo in the overlays folder of the fat32 partition

copy Pi400VGA-config.txt in the crt/dacs folder of the fat32 partition

ssh recalbox

    cd /
    mount -o remount,rw /
    cd /lib/modules/5.10.83-v7l/extra/
    cp /boot/overlays/recalboxrgbdual.ko recalboxrgbdual.ko
    chmod 644 rpi-dpidac.ko
    
reboot


[:fr:](LISEZMOI.md) [:uk:](README.md)

# Pi400VGA
interface VGA pour Raspberry Pi 400

achetez sur [ebay](https://www.ebay.fr/itm/) :package:

![](img/Pi400VGA.jpg)

### DPI (Display parallel Interface)
Ce montage utilise le mode 3 dpi, 

![](img/dpi-packing.png)

voir https://www.raspberrypi.org/documentation/hardware/raspberrypi/dpi/README.md

seuls les bits nécessaires du dpi sont redirigées sur le port GPIO 40 broches, avec la ligne 'gpio=2-8,12-17,20-24=a2' dufichier config.txt 

/boot/config.txt

    # disable i2c, pin use by h-sync & v-sync
    dtparam=i2c_arm=off
    gpio=2-8,12-17,20-24=a2
    dpi_output_format=0x13
    enable_dpi_lcd=1
    display_default_lcd=1
    dpi_group=2
    dpi_mode=16
    #---------------- dpi_mode line ---------------------
    #---> 640x480 60hz    dpi_mode=4
    #---> 800x600 60hz    dpi_mode=9
    #---> 1024x768 60hz   dpi_mode=16
    #---> 1280x768 60hz   dpi_mode=23
    #---> 1280x800 60hz   dpi_mode=28
    #---> 1280x960 60hz   dpi_mode=32
    #---> 1280x1024 60hz  dpi_mode=35
    #---> 1360x768 60hz   dpi_mode=39
    #---> 1366x768 60hz   dpi_mode=81
    #---> 1400x1050 60hz  dpi_mode=42
    #---> 1440x900 60hz   dpi_mode=47
    #---> 1600x1200 60hz  dpi_mode=51
    #---> 1680x1050 60hz  dpi_mode=58
    #---> 1920x1080 60hz  dpi_mode=82
    #---> 1920x1200 60hz  dpi_mode=69
    #---> 1920x1440 60hz  dpi_mode=73    
    
### Double Ecran (VGA + HDMI)

:warning: nécessite raspbian buster

editer le fichier /boot/config.txt  

ajouter, à la fin du fichier, les lignes:

    [all]
    #dtoverlay=vc4-fkms-v3d
    max_framebuffers=2


editer le fichier /usr/share/X11/xorg.conf.d/99-fbturbo.conf

     This is a minimal sample config file, which can be copied to
    # /etc/X11/xorg.conf in order to make the Xorg server pick up
    # and load xf86-video-fbturbo driver installed in the system.    
    #
    # When troubleshooting, check /var/log/Xorg.0.log for the debugging
    # output and error messages.
    #
    # Run "man fbturbo" to get additional information about the extra
    # configuration options for tuning the driver.
    
    #Section "Device"
    #        Identifier      "Allwinner A10/A13 FBDEV"
    #        Driver          "fbturbo"
    #        Option          "fbdev" "/dev/fb0"
    #        Option          "SwapbuffersWait" "true"
    #EndSection
    
    Section "Device"
    Identifier "Raspberry Pi HDMI"
    Driver "fbturbo"
    Option "fbdev" "/dev/fb0"
    Option "ShadowFB" "off"
    EndSection
    
    Section "Device"
    Identifier "Raspberry Pi DPI"
    Driver "fbturbo"
    Option "fbdev" "/dev/fb1"
    Option "ShadowFB" "off"
    EndSection
    
    Section "Monitor"
    Identifier "HDMI"
    EndSection

    Section "Monitor"
    Identifier "DPI"
    EndSection
    
    Section "Screen"
    Identifier "screen0"
    Device "Raspberry Pi HDMI"
    Monitor "HDMI"
    EndSection
    
    Section "Screen"
    Identifier "screen1"
    Device "Raspberry Pi DPI"
    Monitor "DPI"
    EndSection
    
    Section "ServerLayout"
    Identifier "default"
    Screen 0 "screen0" 0 0
    Screen 1 "screen1" RightOf "screen0"
    Option "Xinerama" "on"
    EndSection

### Bureau à distance en double écrans

installation de freeRDP

    sudo apt-get install freerdp2-x11

lancement d'un session freeRDP
    
    xfreerdp /v:<nom ou IP de l'ordinateur> /u:<utilisateur> /d:<domaine> /sound:sys:alsa /multimon

or

    xfreerdp /v:<nom ou IP de l'ordinateur> /u:<utilisateur> /d:<domaine> /g:<nom ou IP de la passerelle RDP> /gu:<utilisateur de la passerelle> /gd:<domaine de la passerelle> /sound:sys:alsa /multimon

### Interface audio
le son est généré en MLI (PWM) à partir des broches gpio 18 & 19

/boot/config.txt

    # Enable audio on GPIO for Pi 400
    dtoverlay=audremap,pins_18_19
    dtparam=audio=on
    
## Schéma & Circuit Imprimé
![sch](img/sch.PNG)

![pcb](img/3D.PNG)

## Installation
Copier le contenu du fichier [config-example.txt](img/config-example.txt?raw=true) dans le fichier /boot/config.txt

## Révision
rev1


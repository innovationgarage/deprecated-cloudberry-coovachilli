# Chilli Access Controller On Raspberry Pi Model B V1.2

This is a step by step guide to turn your Raspberry Pi device into a Chilli
access controller. Please have the following items prepared before starting

- The Pi.
- Compatible power usb cable.
- USB power hub.
- USB ethernet.
- Compatible tp-link wifi USB adapter>
- USB Keyboard.
- HDMI monitor and cable.
- SDcard.


## Installing LEDE

Download the [lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img.gz][img]

    $ wget https://downloads.lede-project.org/releases/17.01.4/targets/brcm2708/bcm2710/lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img.gz

Uncompress the archive

    $ gunzip -d lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img.gz

Flash the SDcard with the image

    $ sudo dd bs=1m if=lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img of=/dev/rdisk2 conv=sync

## Getting Chilli

When the device boots up with the brand new install, make some temporary network changes.
Like making lan use dhcp:

    # /etc/config/network
    # Change only the lan section to look like
    config interface 'lan'
        option ifname 'eth0'
        option proto 'dhcp'

Restart the network for the changes to take effect and plug in a ethernet cable to the onboard ethernet port

    $ /etc/init.d/network restart

Install git and other dependencies

    $ opkg update
    $ opkg install git-http ca-certificates ca-bundle libustream-openssl haserl

Prepare chilli setup

    $ /etc/init.d/dnsmasq disable
    $ /etc/init.d/dnsmasq stop
    $ git clone https://github.com/innovationgarage/cloudberry-coovachilli
    $ cp -r cloudberry-coovachilli/etc/chilli /etc/chilli
    $ cp  cloudberry-coovachilli/etc/config/* /etc/config

Before procedding to installing chilli 

    # Verify the radiussecret and uamsecret in /etc/config/chilli is correct
    # Verify the HS_RADSECRET and HS_UAMSECRET in /etc/chilli/defaults is correct

Install chilli

    $ opkg install coova-chilli
    # The chilli config warnings can be ignored.
    $ reboot

## Hardware setup

1. Connect the USB wifi adapter to the power hub.
2. Connect the power hub to the Pi.
3. Connect the USB ethernet to the PI.
4. Connect keyboard to the PI.
5. Connect HDMI monitor to the PI.

[img]: https://downloads.lede-project.org/releases/17.01.4/targets/brcm2708/bcm2710/lede-17.01.4-brcm2708-bcm2710-rpi-3-ext4-sdcard.img.gz

## Useful links

- [OpenWrt/LEDE wiki - Raspberry Pi](https://wiki.openwrt.org/toh/raspberry_pi_foundation/raspberry_pi)
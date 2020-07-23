# Update Raspberry Pi 4 Firmware on a Ubuntu 20.04 ARM64 Installation

1. Add additional PPA repository for Raspberry Pi utilities

```bash
    sudo add-apt-repository ppa:ubuntu-raspi2/ppa
    sudo add-apt-repository ppa:ubuntu-pi-flavour-makers/ppa
    sudo apt-get update
```

If you see `E: The repository 'http://ppa.launchpad.net/ubuntu-raspi2/ppa/ubuntu focal Release' does not have a Release file.` error message, which means the first ppa repository does not have focal releases yet, change it to the last release version.

```bash
    sudo sed -i "s/focal/bionic/g" /etc/apt/sources.list.d/ubuntu-raspi2-ubuntu-ppa-focal.list
    sudo apt update
```

2. Install Raspberry Pi utility packages

```bash
    sudo apt install libraspberrypi-bin libraspberrypi-dev rpi-eeprom
```

3. Update firmware using the `rpi-eeprom-update` command

```bash
    $ sudo rpi-eeprom-update
    BCM2711 detected
    Dedicated VL805 EEPROM detected
    *** UPDATE REQUIRED ***
    BOOTLOADER: update required
    CURRENT: Mon Jul 15 12:59:55 UTC 2019 (1563195595)
    LATEST: Thu Apr 16 17:11:26 UTC 2020 (1587057086)
    FW DIR: /lib/firmware/raspberrypi/bootloader/critical
    VL805: update required
    CURRENT: 00013701
    LATEST: 000137ad

    $ sudo rpi-eeprom-update -a
    BCM2711 detected
    Dedicated VL805 EEPROM detected
    BOOTFS /boot/firmware
    *** INSTALLING EEPROM UPDATES ***
    BOOTLOADER: update required
    CURRENT: Mon Jul 15 12:59:55 UTC 2019 (1563195595)
    LATEST: Thu Apr 16 17:11:26 UTC 2020 (1587057086)
    FW DIR: /lib/firmware/raspberrypi/bootloader/critical
    VL805: update required
    CURRENT: 00013701
    LATEST: 000137ad
    BOOTFS /boot/firmware
    EEPROM updates pending. Please reboot to apply the update.

    $ sudo reboot

    ...

    $ sudo rpi-eeprom-update
    BCM2711 detected
    Dedicated VL805 EEPROM detected
    BOOTLOADER: up-to-date
    CURRENT: Thu Apr 16 17:11:26 UTC 2020 (1587057086)
    LATEST: Thu Apr 16 17:11:26 UTC 2020 (1587057086)
    FW DIR: /lib/firmware/raspberrypi/bootloader/critical
    VL805: up-to-date
    CURRENT: 000137ad
    LATEST: 000137ad
```

4. Update GPU firmware and bootloaders

```bash
    sudo apt upgrade linux-firmware-raspi2
    sudo reboot
```

## Reference Links

1. [Ubuntu Raspberry Pi Wiki](https://wiki.ubuntu.com/ARM/RaspberryPi)

2. [Ubuntu Pi Flavour Maker Team](https://launchpad.net/~ubuntu-pi-flavour-makers/+archive/ubuntu/ppa)
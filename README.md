# pi-misc-conf

## Setup
```shell
sudo ln -s $PWD/boot/config.txt /boot
sudo ln -s $PWD/etc/modprobe.d/bcm2835-wdt.conf /etc/modprobe.d
```

## How to see if a watchdog timer works properly
First, check the logs.

```shell
sudo dmesg | grep bcm2835-wdt
sudo dmesg | grep systemd | grep watchdog
```

```
[    1.949143] bcm2835-wdt bcm2835-wdt: Broadcom BCM2835 watchdog timer
```

```
[    9.389119] systemd[1]: Using hardware watchdog 'Broadcom BCM2835 Watchdog timer', version 0, device /dev/watchdog
[    9.401138] systemd[1]: Set hardware watchdog to 5s.
```

Then, try dropping a fork bomb.

```shell
:(){ :|:& };:
```

If the watchdog timer works fine, the system should reboot automatically in a couple of minutes.

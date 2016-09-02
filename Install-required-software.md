[First Steps](#first-steps)<br>
[Basic Packages](#basic-packages)<br>
[Install LIRC](#install-lirc)<br>
[Python libs for GPIO SPI and I2C](#python-libs-for-gpio-spi-and-i2c)<br>
[Python support for rotary encoder](#python-support-for-rotary-encoder)<br>
[Python Input Event Interface](#python-input-event-interface)<br>
[MPD and python support](#mpd-and-python-support)<br>
[Pygame](#pygame)<br>
[Python WIFI lib](#python-wifi-lib)<br>
[Systemd Python](#systemd-python)<br>
[SPI Display](#spi-display)<br>
[Shairport](#shairport)<br>
[Bootsplash](#bootsplash)<br>

### First steps
- Start with a RASPBIAN JESSIE LITE image from the [Raspbian download page](https://www.raspberrypi.org/downloads/raspbian/)
- use raspi-config to set hostname, timezone and local settings. Also enable i2c and spi interfaces.   
- create a install directory cd into it
```
mkdir /install
cd /install
```
- Bring everything up to date
```
apt-get update
apt-get upgrade
apt-get install rpi-update
rpi-update
reboot
```
### Basic Packages
```
apt-get install git
apt-get install python-pip
apt-get install python-setuptools python-dev
```

### Install LIRC
```
apt-get install lirc
```

### Python libs for GPIO SPI and I2C
```
pip install WiringPi2
pip install spidev
apt-get install i2c-tools
apt-get install python-smbus
apt-get install libi2c-dev
```

### Python support for rotary encoder
```
cd /install
git clone https://github.com/guyc/py-gaugette
cd py-gaugette/
python setup.py install
```

### Python Input Event Interface
```
pip install evdev
```

### MPD and python support
```
apt-get install mpd
apt-get install mpc
apt-get install python-mpd
```

### Pygame
```
apt-get install python-pygame
```

### Python WIFI lib
```
apt-get install libiw-dev
pip install iwlib
```

### Systemd Python
```
cd /install
apt-get install libsystemd-dev
git clone https://github.com/systemd/python-systemd
cd python-systemd/
python setup.py install
apt-get install python-dbus
cd /install
git clone https://github.com/abn/python-systemd-dbus
cd python-systemd-dbus/
python setup.py install
```

### SPI Display
```
modprobe fbtft_device name=adafruit22a rotate=270 speed=48000000 fps=50
/etc/modules-load.d/fbtft.conf
/etc/modprobe.d/fbtft.conf
/etc/modprobe.d/alsa-blacklist.conf
con2fbmap 1 1
```

### Shairport
```
cd /install
apt-get install libssl-dev libavahi-client-dev libasound2-dev avahi-daemon
git clone https://github.com/abrasive/shairport.git
cd shairport
./configure
make
make install
cp scripts/debian/init.d/shairport /etc/init.d/
cp scripts/debian/default/shairport /etc/default/
```

### Bootsplash
```
apt-get install fbi
```
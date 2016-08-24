# Installation Notes

[Install basic packages](#basic-packages)<br>
[Install LIRC](#install-lirc)<br>
[Python libs for GPIO SPI and I2C](#python-libs-for-gpio-spi-and-i2c)<br>

### Basic Packages
- apt-get install git
- apt-get install python-pip
- apt-get install python-setuptools python-dev

### Install LIRC
- apt-get install lirc

### Python libs for GPIO SPI and I2C
- pip install WiringPi2
- pip install spidev
- git clone https://github.com/guyc/py-gaugette
- python setup.py install
- pip install evdev
- apt-get install mpd
- apt-get install mpc
- apt-get install python-mpd
- apt-get install python-pygame
- apt-get install libiw-dev
- apt-get install i2c-tools
- apt-get install python-smbus
- apt-get install libi2c-dev
- pip install iwlib
- #apt-get install libsystemd-dev
- #git clone https://github.com/systemd/python-systemd
- #python setup.py install
- apt-get install python-dbus
- git clone https://github.com/abn/python-systemd-dbus
- python setup.py install

- modprobe fbtft_device name=adafruit22a rotate=270 speed=48000000 fps=50
- /etc/modules-load.d/fbtft.conf
- /etc/modprobe.d/fbtft.conf
- /etc/modprobe.d/alsa-blacklist.conf
- con2fbmap 1 1

- apt-get install libssl-dev libavahi-client-dev libasound2-dev avahi-daemon
- git clone https://github.com/abrasive/shairport.git
- cd shairport
- ./configure
- make
- make install
- cp scripts/debian/init.d/shairport /etc/init.d/
- cp scripts/debian/default/shairport /etc/default/
- systemctl enable shairport
- systemctl start shairport
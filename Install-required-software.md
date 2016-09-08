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
[Spotify Connect](#spotify-connect)<br>

### First steps
- Start with a RASPBIAN JESSIE LITE image from the [Raspbian download page](https://www.raspberrypi.org/downloads/raspbian/)
- use raspi-config to set hostname, timezone and local settings. Also enable i2c and spi interfaces.
- configure the network 
- create a install directory and cd into it
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

### Spotify Connect
In order to use the Spotify Connect software you need to have a Spotify Premium account. You also need to obtain an application key at [https://devaccount.spotify.com/my-account/keys/](https://devaccount.spotify.com/my-account/keys/). Download the binary key.

There are several ways to get Spotify connect installed on a Raspberry PI. If you want to get the details you can have a look at the [GipHub page](https://github.com/Fornoth/spotify-connect-web) of the project.
I decided to use the packaged release. This does nor require to install docker for the docker release. The installation from source somehow did not work for me. Here are the steps I used:
```
cd /install
wget https://github.com/Fornoth/spotify-connect-web/releases/download/0.0.2-alpha/spotify-connect-web_0.0.2-alpha.tar.gz
tar zxvf spotify-connect-web_0.0.2-alpha.tar.gz
```
Copy you Spotify application key into /install/spotify-connect-web.

Now there is one problem with my TDA1543 DAC. It does not have any volume control. So Spotify connect software will fail whenever it is trying to access a mixer - it's not there. I got it working by commenting out all lines in the code which do use the mixing device. To make that a bit easier I have some perl commands which have to be executed in the exact order.
```
cd /install/spotify-connect-web
perl -p -i -e 's/, mixer,/, /g' connect.py
perl -p -i -e 's/(.+volume_range)/#$1/g' console_callbacks.py connect.py
perl -p -i -e 's/(.+mixer)/#$1/g' console_callbacks.py connect.py
perl -p -i -e 's/(.+corected_playback_volume)/#$1/g' console_callbacks.py 
```
There is a drawback - the volume control inside the Spotify app does not have any effect anymore.

If you do not want to start the Spotify Connect with your Spotify credentials there is a way to automate that with Zeroconf.
In order to get that working you have to install the apt-get install avahi-utils package and create a little script which is announcing the service and the starts the Spotify Connect software. Place that into /install/spotify-connect-web.
```
apt-get install avahi-utils
vi /install/spotify-connect-web/start_spotify.sh
```
Put into the script:
```
#!/bin/bash
cd /install/spotify-connect-web
/usr/bin/nohup /usr/bin/avahi-publish-service raspiradio3 _spotify-connect._tcp 4000 VERSION=1.0 CPath=/login/_zeroconf &
./spotify-connect-web --bitrate 320 --name raspiradio3
```
To make it work:
```
chmod +x 
/install/spotify-connect-web/start_spotify.sh
```
Now create a systemd unit file:
```
vi /etc/systemd/system/spotify-connect.service
```
Fill it with:
```
[Unit]
Description=Spotify Connect
After=network.target

[Service]
User=root
ExecStart=/install/spotify-connect-web/start_spotify.sh
Restart=always
RestartSec=10
StartLimitInterval=30
StartLimitBurst=20

[Install]
WantedBy=multi-user.target
```
And enable it:
```
systemctl enable spotify-connect
```
The software is still under development and not perfect at all. That's why there is still no Debian package available. The systemd service files still assume that everything is located under /install/raspiradio. If there is an interest in making that easier please let me know. If you want to know more why some things are done please have a look at the 
[useful information page](https://github.com/thk4711/raspiradio/wiki/Useful-Information).
___

[Clone the git repository](#clone-the-git-repository)<br>

### Configure SPI frame buffer
Raspbian does support a lot of small mostly SPI based displays which are available on eBay for little money. Please have a look at the [project Wiki](https://github.com/notro/fbtft/wiki).
In order to make use of it you have to load and configure the frame buffer kernel module. The settings, which do reflect my display are part of the repository.

The fbtft.conf file contains the parameters, which are used when the frame buffer kernel module is loaded. They define which display is used and which GPIO pins are used for reset, abcligt e.t.c.
```
cp /install/raspiradio/os-files/etc/modprobe.d/fbtft.conf etc/modprobe.d/
```
To load the module at boot copy this file:
```
cp /install/raspiradio/os-files/etc/modules-load.d/fbtft.conf /etc/modules-load.d/fbtft.conf
```
To test if it is working - first load the module.
```
modprobe fbtft_device
```
... and the start a text console.
```
con2fbmap 1 1
```
If you now do see a login prompt you are done with the setup of the display.

### Setup the I2S sound output
The defoult sound output on a Raspberry pi is the one on the Broadcom SOC. If we want to use I2S sound we first need to set this up in the /boot/config.txt .
There is support for various chips in the case of the the TDA1543 the following is relevant:
```
 # enable hifi dac
device_tree_overlay=hifiberry-dac
```
If you want to use another I2S sound card this might be different.
Now we have to avoid that the default sound module gets loaded. To do this, we need the file /etc/modprobe.d/alsa-blacklist.conf.
```
cp /install/raspiradio/os-files/etc/modprobe.d/alsa-blacklist.conf /etc/modprobe.d/
```
Now reboot. 
To check weather everything is OK enter the command
```
aplay -l
```
... the output should look like this:
```
**** List of PLAYBACK Hardware Devices ****
card 0: sndrpihifiberry [snd_rpi_hifiberry_dac], device 0: HifiBerry DAC HiFi pcm5102a-hifi-0 []
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```
### Clone the git repository
```
cd /install
git clone https://github.com/thk4711/raspiradio
```


### Create your playlist
The mpd software, which is used to play the internet radio stations, needs a playlist file in the m3u format. The file has to be /var/lib/mpd/playlists/radio.m3u
An example is in /install/raspiradio/os-files/var/lib/mpd/playlists/radio.m3u

### Create shutdown systemd services
If you want to shutdown the raspberry with a signal on a GPIO pin you need to enable this service. If you do not intend to do this you can skip this step. 
```
cp /install/raspiradio/os-files/etc/systemd/system/radio-shutdown.service /etc/systemd/system/
systemctl enable radio-shutdown
systemctl start radio-shutdown
```

### Create bootsplash systemd services
This service will show the Raspberry Pi logo as early as possible in the boot process. The image which is shown is located at /install/raspiradio/Images/raspilogo.jpg
```
cp /install/raspiradio/os-files/etc/systemd/system/bootsplash.service /etc/systemd/system/
systemctl enable bootsplash
```
If you want a different logo you can create a jpeg image at the resolution of the TFT display (320x240 in my case).
You have to edit the /etc/systemd/system/bootsplash.service file to display your own image.

### Create radio systemd services
This service will run the actual radio software. If it should crash it will be automatically restarted.
```
cp /install/raspiradio/os-files/etc/systemd/system/radio.service /etc/systemd/system/
systemctl enable radio
systemctl start radio
```
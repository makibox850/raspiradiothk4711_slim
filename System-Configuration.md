The software is still under development and not perfect at all. That's why there is still no Debian package available. The systemd service files still assume that everything is located under /install/raspiradio. If there is an interest in making that easier please let me know.

[Clone the git repository](#clone-the-git-repository)<br>

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
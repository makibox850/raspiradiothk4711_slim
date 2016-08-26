

[Raspberry Infrared (LIRC)](#infrared-remote-control-with-lirc)<br>
[I2S Audio](#i2s-audio)<br>
[TDA1543 DAC](#tda1543-dac)<br> 
[SD Card Overclocking](#sd-card-overclocking)<br> 
[Frame buffer display](#frame-buffer-display)<br>
[Rotary Encoder Python](#rotary-encoder-python)<br>
[GPIO Python](#gpio-python)<br>
[MPD Python](#mpd-python)<br>
[Airplay](#airplay)<br>
[Spotify Connect](#spotify-connect)<br>
[Python UI](#python-ui)<br>
[Power Supply](#power-supply)

### Infrared remote control with LIRC
- Hardware for LIRC and kernel konfiguration - http://aron.ws/projects/lirc_rpi/
- LIRC on non default GPIO - http://www.forum-raspberrypi.de/Thread-lirc-auf-anderen-gpio-port-legen
- general HOWTO - http://indibit.de/raspberry-pi-mit-apple-remotelirc-python-scripte-steuern/
- general lirc setup: http://aron.ws/projects/lirc_rpi/

### I2S Audio
- http://www.dimdim.gr/2014/12/the-rasberry-pi-audio-out-through-i2s/
- http://www.runeaudio.com/forum/i2s-connection-to-an-external-dac-t1337.html
- /boot/config.txt overlay: http://www.runeaudio.com/forum/audiophonics-dac-sabre-es9023-i2s-24bit-192-raspberry-pi-t1155-10.html
- wiring b+, PI2/3: http://www.pagemac.com/projects/i2s_amp
- wiring ald raspi: http://www.tjaekel.com/T-DAC/pictures/Rpi_P5_I2S_small.png

### TDA1543 DAC
- simple schematics - http://www.pavouk.org/hw/modulardac/en_tda1543.html
- If you want to know more - http://www.dddac.de/start.html

### SD Card Overclocking
- http://www.jeffgeerling.com/blog/2016/how-overclock-microsd-card-reader-on-raspberry-pi-3

### Frame buffer display
- project home page - https://github.com/notro/fbtft/wiki
- the display I am using - http://4.bp.blogspot.com/-IBUfOEStb6A/VIZiPWw9rMI/AAAAAAAAVT0/TYKj5dCf0Zo/s1600/raspberrypi_TFTLCD_wiring1.png
- https://rhobobase.wordpress.com/2015/05/01/mini-screen/
- an other one which I have tried - http://sainsmart.tumblr.com/post/52849596106/diagramsainsmart-18-tft-lcd-modules-connect

### Rotary Encoder Python
- howto - http://guy.carpenter.id.au/gaugette/blog/2013/01/14/rotary-encoder-library-for-the-raspberry-pi/
- github page - https://github.com/guyc/py-gaugette

### GPIO Python
- https://sourceforge.net/p/raspberry-gpio-python/wiki/BasicUsage/
- http://wiringpi.com/download-and-install/
- http://raspi.tv/2013/rpi-gpio-basics-4-setting-up-rpi-gpio-numbering-systems-and-inputs

![GPIO PINS](https://github.com/thk4711/raspiradio/blob/master/Images/GPIOPINS-RPI.jpg)

![GPIO PINS](https://github.com/thk4711/raspiradio/blob/master/Images/GPIO-BCM-WIRING.png)

### MPD Python
- https://pythonhosted.org/python-mpd2/
 
### Airplay
- http://www.raspberry-pi-geek.de/Magazin/2015/01/Raspberry-Pi-als-AirPlay-Server-im-Heimnetz
- https://volumio.org/forum/get-spotify-and-airplay-infos-for-lcd-t2420.html

### Spotify Connect
- http://www.forum-raspberrypi.de/Thread-tutorial-spotify-connect-server-headless-standalone

### Python UI
- https://learn.adafruit.com/raspberry-pi-pygame-ui-basics
- http://nullege.com/codes/search/pygame.font.Font.render

### Power Supply
- http://www.wenzel.com/documents/finesse.html
- http://www.analog.com/library/analogdialogue/archives/46-06/staying_well_grounded.html
- https://embeddedcode.wordpress.com/2013/10/18/adding-a-shutdown-button-to-the-raspberry-pi/
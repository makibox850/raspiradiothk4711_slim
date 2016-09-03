[General](#general)<br>
[Display lib](#display-lib)<br>
[Audio lib](#audio-lib)<br>
[Input lib](#input-lib)<br>
[Other services](#other-services)<br>
[Shutdown service](#shutdown-service)

### General
The software is completely written in python because the on Raspbian it seems to be the programming language which has the best documentation how to interact with the hardware. Since this is my first significant software project it is for sure not optimal. So if you identify room for improvement, let me know ;-)

Almost everything is handled directly in python. The main programm is in /install/raspiradio/python/radio.py . Some components are in a separate python lib. the are in /install/raspiradio/python/lib . In oder to have some nice looking fonts and icons I am using ttf fonts they are in /install/raspiradio/python/fonts. I was trying not to call OS commands to avoid dependencies from the existence and version of other software. 

The goal was also to give others the chance to get this to work with other hardware. That's why the following things are handled by a module in oder to allow others to write their own for different display, sound controls and cases.

### Display lib
The display library is used to handle the display on the device. I have only implemented a frame buffer device based display which has to be supported by the kernel. In my case it is a 320x240 SPI device from eBay. Other devices should work as well with my code, because the resolution is auto detected and the scaling depends on the resolution of the display. And since the fonts are ttf fonts they should also scale nicely. The drawing and painting is handled by the pygame framework, which was very helpful for me.

But there is no need to use a tft display it would also be possible to use for instance a HD44780 based character display. There is also no need to display everything. Just do not do anything with the date and it's OK as well.

### Audio lib
The audio module does handle the following functions:
- Volume control
- Tone control
- Switch audio source (USB, AUX, Raspi)

Since I was experimenting with some different chips I have modules for the following chips:
- MS6714 from Mosanalog - this chip does also have an integrated source switch but no middle control. This chip is a clone of the PT2314 chip, which for some reason does not work with the I2C raspberry interface. There is a module with the PT2314 available on Aliexpress (if you do not want to make your own). But in order to use it you would have to exchange the chip.
- TDA7439 from Philips - this chip does also include a source switch. What I did not like was that the steps of the volume control were a little bit coarse.
- PT2322 - this is the chip I ended up using in my device. It is actually a 6 channel chip but I am only using 2 channels. The drawback is that it does not have an integrated source switch. I am using 2 relays which are controlled by a I2C based IO chip (PCF8574). 

The first 2 modules are not well tested because I gave up using these chips.

But also here it is possible to do something completely different. If you are not so much concerned about sound quality you might just use alsa and alsaequal to de everything in software und only use the built in audio of the raspberry.

### Input lib
This library is handling all user input to trigger actions in the main program. In my case it is the front panel of the Yamaha case and the Apple Remote.

### Other services
The internet radio is handled by mpd. There is a python module which I am using to interact with it. For Airplay I am using shairport. Spotify connect works like decribed here. The services are turned on and of as needed. If you want to use something else you just need to find out how to use it on a raspberry. It is very easy to integrate this in the software. 

Some might ask - why no bluetooth ? There are 2 reasons for that:
- I was not able to find out how to get a bluetooth audio sink working with alsa and the current version of the bluetooth stack in Debian.
- The audio quality of bluetooth is worse than Airplay and spotify connect.

### Shutdown service
This service is used to shut the Raspberry Pi down in a controlled manner based on a GPIO pin pulled to ground. The scrip which is doing this is at /install/raspiradio/python/shutdown.py
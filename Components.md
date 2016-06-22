### Raspberry PI:
Everything in this Radio is controlled by a raspberry pi. Actually every model should be working. I have tested it on a Raspberry PI 2, a Raspberry PI 3 and a Raspberry Pi Zero. But also older models should be OK. Just be aware that the I2S audio output will be different on old Raspberry Pi models.

### SD Card:
Since we do not need a full blown GUI a minimal Raspbian image would be good enough. For that anything with a size of 2GB or greater would be OK. If you are concerned about boot speed and reliability I do recommend to use SanDisk Extreme or Samsung PRO cards. Cheep cards tend to fail and often are very slow.

### Wi-Fi USB:
Unless you are using a Raspberry Pi 3 or you prefer Ethernet - you will need a USB Wi-Fi adapter. There are many available and most should work. I have tried some and came to the conclusion that it makes no sense to spend a lot of money for it. Some expansive ones are good some are bad and with the cheep ones it is the same. The biggest difference for this use case are: 
- the range: here I prefer adapters with the ability to connect an antenna. If you want to put the radio into a metal case you will need that, to be able to connect a extension cable. 
- the noise it introduces to the audio signal: Here I do not fully understand why some adapter introduce audible noise even into the digital i2s signal - but it is the case. 
The best option I have found is the following device: [150Mbps USB WiFi Wireless Adapter LAN w/ Antenna Raspberry Pi Ralink RT5370](http://www.ebay.com/itm/150Mbps-USB-WiFi-Wireless-Adapter-LAN-w-Antenna-Raspberry-Pi-Ralink-RT5370-/181769887414?hash=item2a52545eb6:g:z5gAAOSwrklVd5yq) on eBay. It comes directly from Hong Kong and it is about 6$ including shipping.  
![Wi-Fi-USB](https://github.com/thk4711/raspiradio/blob/master/Images/Wi-Fi.jpg)

### Proto HAT Shield for Raspberry Pi
Since we will have to connect many things to the Raspberry GPIO's such a shield will allow us to create some nice connectors for ribbon cables. It is not absolutely necessary - the wires can be connected to the GPIO header but it looks much nicer.
[DIY Proto HAT Shield for Raspberry Pi 2 Model B / B+ / A+](http://www.aliexpress.com/item/DIY-Proto-HAT-Shield-for-Raspberry-Pi-2-Model-B-B-A-Red-free-shipping/32593336989.html) This comes with everything you need for less than 4$ from AliExpress. I think on eBay they are for sale as well.
![Proto Hat](https://github.com/thk4711/raspiradio/blob/master/Images/protohat.jpg)

### 16 Bit I2C 4 Channel ADS1115 AD converter
The Yamaha HiFi tuner case I am using has a front panel with many switches. They are divided in 3 groups. All switches are connected over a resistor and pull the connection to ground on each crossing. With that you can create a voltage divider which delivers a different voltage for every switch you press. Unfortunately the Raspberry Pi does not come with a AD converter, we need to add an external unit. The ADS1115 is a chip which can be talked to using I2C. There are my little bord available on eBay like this one: [16 Bit I2C 4 Channel ADS1115](http://www.ebay.com/itm/For-Arduino-ADS1115-Module-4-Channel-16-Bit-I2C-ADC-With-Pro-Gain-Amplifier-/221980694555?hash=item33af14981b:g:15QAAOSwT~9WlHfX) - will be less that 3$
If you are not planning to use a case like I did you might not need this.
![ADS1115](https://github.com/thk4711/raspiradio/blob/master/Images/ads1115.jpg)

### IR Receiver
If you want to use a IR Remote you need a IR reviver. Just look at eBay for something like this: [ IR Receiver Module 38 kHz TSOP4838 ](http://www.ebay.com/itm/IR-Receiver-Infrared-Radiation-Module-38-kHz-Remote-TSOP4838-DIP-3-/222087090405?hash=item33b56c10e5:g:kFgAAOSwD0lUcF9g) 
![IR](https://github.com/thk4711/raspiradio/blob/master/Images/ir-receiver.jpg)

### TFT Display
The radio is using a small 2.2' SPI Display. This unit dies also have a SC card slot which we do not use here. For my Yamaha case I hd to replace the strait terminals with 90 degree terminals because they did not fit underneath the circuit board. In general there are many displays you can use please check [the following link](https://github.com/notro/fbtft/wiki) for Displays which are supported by the raspbian kernel. You can get these mostly on eBay or AliExpress for less than 10$. The page also has many useful information how to set it up and how to test it.
[2.2 inch 2.2" SPI TFT LCD Display module 240x320 ILI9341 51/AVR/STM32/ARM/PIC](http://www.ebay.com/itm/2-2-inch-2-2-SPI-TFT-LCD-Display-module-240x320-ILI9341-51-AVR-STM32-ARM-PIC-/311569442127?hash=item488afc654f:g:B2oAAOSwT5tWPHt7)
![tft display](https://github.com/thk4711/raspiradio/blob/master/Images/tft-display.jpg)

### WiFi antenna extension
Since I am using a metal case for the radio a antenna within that case would be not a good idea. I am using the above mentioned USB WiFi adapter which dies allow the connection of this extension cable, that is mounted into a hole in the back of the case. The antenna itself can be reused there. [WiFi Antenna EXTENSION Cable/Lead Wireless RP SMA male to female 4 in to 10 feet](http://www.ebay.com/itm/WiFi-Antenna-EXTENSION-Cable-Lead-Wireless-RP-SMA-male-to-female-4-in-to-10-feet-/162073692670?var=&hash=item25bc5849fe:m:mWh-vrnI_sL20h2vfbIT3YQ)
![antenna cable](https://github.com/thk4711/raspiradio/blob/master/Images/antenna-cable.jpg)

### Power Supply
When I started that project I was not aware that this actually was the most complicated part of the Hardware design. 



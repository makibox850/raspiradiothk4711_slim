### Raspberry PI:
Everything in this Radio is controlled by a raspberry pi. Actually every model should be working. I have tested it on a Raspberry PI 2, a Raspberry PI 3 and a Raspberry Pi Zero. But also older models should be OK. 

### SD Card:
Since we do not need a full blown GUI a minimal Raspbian image would be good enough. For that anything with a size of 2GB or greater would be OK. If you are concerned about boot speed and reliability I do recommend to use SanDisk Extreme or Samsung PRO cards. Cheep cards tend to fail and often are very slow.

### Wi-Fi USB:
Unless you are using a Raspberry Pi 3 or you prefer Ethernet - you will need a USB Wi-Fi adapter. There are many available and most should work. I have tried some and came to the conclusion that it makes no sense to spend a lot of money for it. Some expansive ones are good some are bad and with the cheep ones it is the same. The biggest difference for this use case are: 
- the range: here I prefer adapters with the ability to connect an antenna. If you want to put the radio into a metal case you will need that, to be able to connect a extension cable. 
- the noise it introduces to the audio signal: Here I do not fully understand why some adapter introduce audible noise even into the digital i2s signal - but it is the case. 

The best option I have found is the following device: [150Mbps USB WiFi Wireless Adapter LAN w/ Antenna Raspberry Pi Ralink RT5370](http://www.ebay.com/itm/150Mbps-USB-WiFi-Wireless-Adapter-LAN-w-Antenna-Raspberry-Pi-Ralink-RT5370-/181769887414?hash=item2a52545eb6:g:z5gAAOSwrklVd5yq) on eBay. It comes directly from Hong Kong and it is about 6$ including shipping.  

### Proto HAT Shield for Raspberry Pi
Since we will have to connect many things to the Raspberry GPIO's such a shield will allow us to create some nice connectors for ribbon cables. It is not absolutely necessary - the wires can be connected to the GPIO header but it looks much nicer.
[DIY Proto HAT Shield for Raspberry Pi 2 Model B / B+ / A+](http://www.aliexpress.com/item/DIY-Proto-HAT-Shield-for-Raspberry-Pi-2-Model-B-B-A-Red-free-shipping/32593336989.html) This comes with everything you need for less than 4$ from AliExpress. I think on eBay they are for sale as well.
![Proto Hat](https://github.com/thk4711/raspiradio/blob/master/Images/protohat.jpg)

### 16 Bit I2C 4 Channel ADS1115 AD converter
The Yamaha HiFi tuner case I am using has a front panel with many switches. They are divided in 3 groups. All switches are connected over a resistor and pull the connection to ground on each crossing. With that you can create a voltage divider which delivers a different voltage for every switch you press. Unfortunately the Raspberry Pi does not come with a AD converter, we need to add an external unit. The ADS1115 is a chip which can be talked to using I2C. There are my little bord available on eBay like this one: [16 Bit I2C 4 Channel ADS1115](http://www.ebay.com/itm/For-Arduino-ADS1115-Module-4-Channel-16-Bit-I2C-ADC-With-Pro-Gain-Amplifier-/221980694555?hash=item33af14981b:g:15QAAOSwT~9WlHfX) - will be less that 3$
If you are not planning to use a case like I did you might not need this.

### IR Receiver
If you want to use a IR Remote you need a IR reviver. Just look at ebay for something like this: [ IR Receiver Module 38 kHz TSOP4838 ](http://www.ebay.com/itm/IR-Receiver-Infrared-Radiation-Module-38-kHz-Remote-TSOP4838-DIP-3-/222087090405?hash=item33b56c10e5:g:kFgAAOSwD0lUcF9g) 
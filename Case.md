Cases are always a bit of a problem. In order to make a good one you need a well equipped workshop and you also need to know how to use all the tool. I am not very good at this at all. That's why I decided to reuse the case of broken HIFI equipment. These are way better than anything I would be able to fabricate. I got a broken Yamaha TX-590 RDS HIFI Tuner. 
![Client_without_speaker](https://github.com/thk4711/raspiradio/blob/master/Images/Client_without_speaker.jpg)
It has a lot of push buttons large display and a rotary encoder. In oder to reuse the buttons I examined the circuit board behind the front panel. There were 3 groups of buttons. They did end up on a pin of a chip on the original board. I broke that connection by removing 3 wire bridges. One pin of each button was connected to one pin of the next button using a resistor. On the junction points every button could pull this point to ground. To read that I am using a AC converter module based on a ADS1115 chip. You can communicate with it using I2C. At the end of each group of switches I added 2 resistors on to ground and one to 3.3V. This does result in a voltage between 3.3 and 0 V. When I press a button now I add a parallel resistor to ground. The value depends on which button I press, because there are more or less resistors in between. That now changes the voltage divider depending on which button is pressed - resulting in a different voltage. This can be measured with the AD converter. Since there are 3 groups I need 3 of them.

The rotary encoder is working just fine with the raspberry Pi - so we can keep it. 

The original VFT display was not usable - so I removed it from the board and replaced it with 320x240 SPI TFT display.

The back panel of the yamaha tuner also had to be replaced because I needed different connectors. That was easy because the old one was attached just with 2 screws.
![client_back](https://github.com/thk4711/raspiradio/blob/master/Images/Client_open_back.jpg)
After everything is put together and the cover is closed it basically still looks the same like before. It just serves a entirely different purpose.

![top_view](https://github.com/thk4711/raspiradio/blob/master/Images/Client_open_top.jpg)
When I started the project my plan for the power supply was to use a 12V 5A switching power supply and 2 step down modules from eBay to generate the 5V for the raspi and the 7V for the analog board. Unfortunately that was not a good idea. With this configuration I was not able to get a good audio signal. There was always "digital" noise in the audio path. 

After reading a lot (please also see the [Useful information](useful-information#power-supply) about that topic I found that the problem is mostly caused by the fact that the digital components generate noise in the analog part because the current of all components did have a common ground. And where current is there is also a voltage drop. And even if it is very low - you can here it.

So after all I ended up with a much more complex power supply than I wanted to have. In fact the power supply turned out to be the most difficult part of the device.

The power supply does provide 3 independent DC sources with 2 toroidal transformers. 

For audio applications traditional transformers and linear regulators perform better that switching power supplies.  

### Transformers
- The first transformer (RKPT 25207) does provide 2x7V AC at 1785 mA. One is used for the digital components. The second one is used for all the analog components except the power amplifier.
- The second transformer is a toroidal transformer Sedlbauer. It provides 2x12V AC at 5A. This transformer does provide the power for the power amplifier board.

### Power Supply Board
![Power_Supply_Board](https://github.com/thk4711/raspiradio/blob/master/Images/Power_supply_board.jpg)
On the power supply board there ist the print mounted 2x7V transformer. On of the windings is rectified and 
smoothened with a 4700uF capacitor. The resulting 9V are then reduced to 5V with a [LM2596 based voltage regulator](http://www.ebay.com/itm/1pcs-1-23V-30V-DC-DC-Buck-Converter-Step-Down-Module-LM2596-Power-Supply-Output-/400985220074?hash=item5d5c94e3ea:g:o10AAOxy0x1TVSpD). This voltage is used to power the Raspberry Pi and all other digital components.

![LM2596](https://github.com/thk4711/raspiradio/blob/master/Images/lm2596.jpg)

The voltage from the 12V transformer is rectified and smoothened with 2 4700uF capacitors. That directly feeds the power amplifier board. 
![power-supply-board](https://github.com/thk4711/raspiradio/blob/master/schematics/power-supply-board.png)

### Low Noise Power Supply
The analog part of the device the DAC and the volume/tone control are most sensitive to noise introduced by the power supply. The sound quality suffers a lot if there is a problem. To get the necessary quality I am using [a board from eBay](http://www.ebay.com/itm/12V-24V-Low-Noise-LT1084-Regulator-Power-Supply-Board-for-Tube-AMP-Filament-DAC-/131768499444?hash=item1eae03bcf4:g:MWMAAOSwsN9W~kM8) which does a good job here by using things like high-speed rectifiers, π-type filter circuit, and a LT1084 low dropout voltage regulator.

![LOW-noise-power-supply](https://github.com/thk4711/raspiradio/blob/master/Images/LOW-Noise-Power.jpeg)

The schematics for the power supply:

![low noise schematics](https://github.com/thk4711/raspiradio/blob/master/Images/low-power-schematics.jpeg)

Since the voltage coming out of the transformer is not much higher than the output voltage the heat generated by the linear regulator is not a problem here.

### Power Control Board
![Power_Control_Board](https://github.com/thk4711/raspiradio/blob/master/Images/Power_control_board.jpg)
This board is a little bit a add-on to the project which makes it more convenient and fail save turning the device on and off. Also it helps to get the stand by power consumption low. The problem which is solved with this board ist that it is not a good idea to hard turn of the power of the Raspberry Pi. Sooner or later it will cause a corrupted file system on the SD card and it might no longer boot. But I also did not want to keep it running all the time because it will consume about 3-4W all the time. So I used an Attiny85 micro controller and 2 relays to do that job. The power switch in now indicating which is the desired state of the device. What needs to happen the is controlled by this board. There are 2 relays one is swiching the 240V AC for the power amplifier on and off the 2nd one is switching the 5V DC for the Raspberry PI and the 7V AC for the sound control board. The only thing which is always on ist the small transformer, the 5V step down regulator and the micro controller. That does consume about 0.1W only. The controller is operated by 3.3V which is generated by a little voltage regulator [module from eBay](http://www.ebay.com/itm/5pcs-DC-5V-to-3-3V-Step-Down-Power-Supply-Module-AMS1117-3-3-800MA-LDO-NEW-/181847233524?hash=item2a56f093f4:g:LAMAAOSweW5VWFso), because the Raspberry PI inputs can not handle 5V.

#### When you turn it on the following is happening: 
- when you turn the power switch on Input of the controller is pulled low
- the controller will switch both relays on and the Raspberry will boot into the radio mode

#### When you turn the device off the following is happening:
- The relay controlling the 240V of the 12V transformer for the power amplifier will switch off.
- One output of the controller is going from high to low. It is connected to a GPIO input of the raspberry. There a software is running, which will detect this and gracefully shut down the Raspberry Pi.
- After 10s the power to the raspberry and the sound control board will be shut down as well. This is enough time for the Raspberry to shut down.

![schematics power control board](https://github.com/thk4711/raspiradio/blob/master/schematics/power-control-board.png)
  

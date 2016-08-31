Besides the power supply - the audio board was the only component I put together myself. It has 3 main functions:

- I2S DAC (Digital Analog Converter) 
- Switch between the input sources (Raspberry, AUX, USB)
- Volume and tone control (Treble, Middle, Bass)

All functions are controlled using the I2C bus. Because the I2C interface is not working correctly at 3.3V logic there is a level shift module on the board to push the levels to 5V.

![audio control board](https://github.com/thk4711/raspiradio/blob/master/schematics/audio-board.png)

### I2S DAC
The analog audio output of the Raspberry Pi is known to deliver a very low audio quality. To overcome this there is a way to configure some IO pins as a I2S audio interface. I2S is a protocol developed by Philips in the late 80th to deliver digital sound date between chips. There are a lot of chips available, which do convert this data stream into analog audio. For the raspberry PI there are several board available which do exactly this. They mostly do use more or less current so called over sampling DAC chips. The audio quality is mostly very good and there is nothing wrong using one of these. But I decided to use a very old Phillips chip - TDA1543. I used to have a CD player many years ago which was using exactly this DAC. I always liked the sound of it. It sounds a little more "analog" than the modern chips. This particular chip is a so called non oversampling DAC (NOS). It requires only a couple of external components and does come in a DIP package, which is very convenient for DIY projects.

### Input source switch
To switch between the analog signals the board is using relays which are controlled by a I2C digital IO chip (PCF8574).

### Volume and tone control
To be able to control the volume and the tones with software there are several chips available. Most of them can be controlled using I2C. I evaluated several chips. They all do have their pros and cons. Some do have lower noise some do have a built in input switch. The chip I ended up with is a [PT2322](http://labkit.ru/userfiles/file/documentation/Audioprocessor/pt2322.pdf) from Princeton Technology. It is actually a 6 channel chip but we are using only 2 channels. The advantages of the chip are:
- 3-band tone control (Treble, Middle, Bass)
- Tone defeat function (it is possible to bypass the tone control and use only the volume control)
- DIP package 
- Volume control is possible in 1db steps
- Easily available
- good documentation
- I2C interface  
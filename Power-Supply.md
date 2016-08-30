When I started the project my plan for the power supply was to use a 12V 5A switching power supply and 2 step down modules from eBay to generate the 5V for the raspi and the 7V for the analog board. Unfortunately that was not a good idea. With this configuration I was not able to get a good audio signal. There was always "digital" noise in the audio path. 

After reading a lot about that topic I found that the problem is mostly caused by the fact that the digital components generate noise in the analog part because the current of all components did have a common ground. Add where current is there is also a voltage drop. And even if it is very low - you can here it.

So after all I ended up with a much more complex power supply that I wanted to have. In fact the power supply turned out to be the most difficult part of the device.

The power supply does provide 3 independent DC sources with 2 toroidal transformers. The first transformer does provide 2x7V AC at 1A.  
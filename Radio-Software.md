The software is completely written in python because the on Raspbian it seems to be the programming language which has the best documentation how to interact with the hardware. Since this is my first significant software project it is for sure not optimal. So if you identify room for improvement, let me know ;-)

Almost everything is handled directly in python. The main programm is in /install/raspiradio/python/radio.py . Some components are in a separate python lib. the are in /install/raspiradio/python/lib . In oder to have some nice looking fonts and icons I am using ttf fonts they are in /install/raspiradio/python/fonts.

I was trying to call OS commands to avoid dependencies from the existence and version of other software. The goal was also to give others the chance to get this to work with other hardware. That's why the following things are handled by a module in oder to allow others to write their own for different display, sound controls and cases.
-  
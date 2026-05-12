# Floppy emulator with OSD and selector for the Amiga 600
This is a fusion of a "Gotek" and a "Bluepill" that can provide both FlashFloppy and FF_OSD and also my Amiga-dual-floppy-selector on a single tiny board that fits inside the Amiga 600, under the original floppy drive. Thank you to Keir Fraser for his firmware https://github.com/keirf/FlashFloppy, and to the chinese people for the original device.

Thanks to the OSD and Amiga keyboard support, LCD/OLED display or buttons are no longer necessary and the device can be almost completely hidden inside Amiga computers, without damaging their case. It is still possible to install a display and buttons, though.

In addition, thanks to "Amiga dual floppy selector" feature, it can daisy-chain between the original floppy drive and the motherboard. In this configuration, the OSD let you choose dynamically which drive is DF0 and DF1. You can enjoy both your original games on floppies and disk images on USB or SDcard !

# Disclaimer
This is a hobbyist project, it comes with no warranty and no support. Also remember that the Amiga machines are about 30 years old and may fail because of such hardware expansions.

This version is not endorsed by the author of FlashFloppy, please don't bother him with issues you might have because of it.

I publish my work under the CC-BY-NC-SA license. The content of this repository is the result of weeks of work, requiring investment in tools, parts, prototypes, and risky tests on his own equipment. For this reason the author does not want third parties to sell products and keep all the profit, usually without even offering support to their customers. If you see people selling this without the consent of the author, don't buy from them.

My modifications to the FF_OSD source are under "the unlicense", like the original code.

If you find it useful and want to reward me : I am always looking for Amiga/Amstrad CPC hardware to repair and hack, please contact me.

# BOM
See iBom.

Other boards you may use with it:
- [A600-1200KeyboardSocket](https://github.com/f1ac0/Breakout-and-simple-connector-boards) to pick the keyboard signals on an A600 or A1200
- [USB_A or microSD breakout](https://github.com/f1ac0/Breakout-and-simple-connector-boards) to make the flash memory accessible from outside the system

# Making it
Components are SMD, and have quite thin pin pitch. You need to know what you are doing.

You may choose to install the USB on a remote board, to make them accessible through trapdoors or openings in the case. You may solder buttons, rotary encoder, LED, display and piezo transducer directly : most "pin headers" pads should not be fitted with headers otherwise it will prevent installing the floppy drive over it.

Solder the bottom floppy pin header at the same angle as the drive is installed in the A600. This way the board should be over the back connectors, and the floppy drive connector will fit tightly under the drive. If any doubt, try to install it before soldering.

Check for shorts at least between 5V, 12V and GND traces before applying power ! If it doesn't work after manual soldering, check that all pads are attached and not shorted, good luck!

The programming ports do not need to be soldered since it needs to be programmed just once : you can just hold it in place during the few seconds required for programming.

On the software side, you need to compile FF\_OSD from source, with the small modifications proposed in the "Floppy-emulator-with-OSD" repository. Use `patch -ru -d FF_OSD-master  < patch` to apply them. FlashFloppy does not require any modification.

To program the F103 uC then the F105 uC, I personally use a STLINK clone dongle with the stlink tool : https://github.com/stlink-org/stlink. Each uC has its own SWDIO/SWDCLK pins.

To connect the wires to DRES, MTRX, CSYNC and VIDEO signals on the A600 motherboard without soldering on it, here is a tip:
- Take a metal pin from the female 2.54mm pin socket, which is shaped as a lyre. The one you removed from pin 3 for example.
- Solder the wire on the pin, where you normally solder it.
- Place the pin inside heat-shrink tube, with only 1mm of metal uncovered from the tips of the lyre.
- Snap the tip on the lyre on the inside of the back connector where you need to connect. DRES, MTRX, CSYNC and VIDEO are easily available on the top row of the video and floppy connectors, which is accessible from inside the case!

# Using it
- Plug the floppy ribbon cable on the device ; connect the DRES and MTRX wires on the rear floppy connector ; plug the device on the motherboard floppy connector ; plug the keyboard adapter on U7 (not U13!) ; connect the VIDEO and CSYNC wires on the video connector ; plug the power connectors to the motherboard and to the drive ; Reinstall the drive over it ; manage the USB connector, for axample in place of the modulator.
- Insert the USB thumb drive.
- Turn on the Amiga, enjoy.

To change the drives configuration :
- First you should eject all floppies to prevent confusion of the OS.
- Go to the FF_OSD config menu, change the Drive config setting accordingly. Then Use or Save the new settings.
- If you changed from one to two or two to one drive, then you need to reboot OS for the second drive to be identified or ignored correctly.


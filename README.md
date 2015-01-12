# LEDSerial
### Collection of software for communicating with and controlling individually addressable LED strips

Organized as follows

* arduino - sketch file for arduino controller
* ledcomm - golang library for communicating with arduino controller
* ledmain - sample client for controlling led strip, includes demos
* ledscreen - sample client that projects the screen colors on the led strip

### arduino/SerialSlave

The simplest part of the system, it keeps an internal representation of the LED strip's colors
and supports three commands which are remotely called through a raw serial buffer.

`f` - 1 byte command to flush the internal representation through to the led strip

`c` - 1 byte clear the internal representation of colors and flush it

`s|r|g|b|i` - 5 byte command update a single led in the internal representation. r,g,b,i are 8bit values which
represent the red, green, blue components of the color, and the led index in strip.

In uses the [PololuLedStrip](https://github.com/pololu/pololu-led-strip-arduino) library for communicating with the
LED strip.

The arduino software makes no guarantees about timing or integrity, it plainly read and executes.

### ledcomm

Golang library for communicating with the arduino

### ledmain

![ledmain](http://plankenau.com/i/kmv3AE.gif)

Golang client demo of ledcomm libraries. Can be used to send individual commands to strip

To clear strip

`./ledmain -clear`

To send red to the 5th led

`./ledmain -send -r 255 -g 0 -b 0 -i 5`

To send an HSV color to the 5th led

`./ledmain -send -h 300 -s 1 -v 255 -i 5`

To run the fourth demo at full brightness

`./ledmain -demo -n 4 -brightness 255`

To get the usage help

`./ledmain -help`

### ledscreen

![ledscreen](http://plankenau.com/i/p1CGRY.gif)

Title: Arduino From the Command Line, Revisited
Date: 2100-01-01 00:00
Category: Pages
Tags: Arduino
Slug: arduino-from-the-command-line-revisited
Author: Jeff Irland
Image: DRAFT_stamp.png
Summary: bla bla bla

Check this out

* [Arduino IDE Now Supports Building Software In The Command Line](http://www.lifehacker.com.au/2015/11/arduino-ide-now-supports-building-software-in-the-command-line/)
* [Arduino Development; There’s a Makefile for That](http://hackaday.com/2015/10/01/arduino-development-theres-a-makefile-for-that/)
* [Embed with Elliot: Microcontroller Makefiles](http://hackaday.com/2016/03/15/embed-with-elliot-microcontroller-makefiles/)

# Installing Arduino IDE
[Arduino][11] is an open-source platform used for building electronics projects.
Arduino consists of both a physical programmable circuit board (often referred to as a microcontroller)
and a piece of software, or IDE (Integrated Development Environment) that runs on your computer,
used to write and upload computer code to the physical board.
There is [Linux build of the Arduino IDE][09],
as well as [alternatives to the standard Arduino IDE][10].

You could install tha Arduino IDE via the Ubuntu Software Center and search for Arduino.
Alternatively, you can install via the command line by running the following:

```bash
# install arduino from software repositories
sudo apt-get update && sudo apt-get install arduino arduino-core
```

The above installs a package from the Ubuntu software repositories,
which likely to be an older Arduino IDE version.
The newest version of the Arduino can be downloaded from the [Arduino download page][12].
(**NOTE:** Using this method Arduino software won't automatically be updated,
so you should check Arduino website every few months and download
a new version if one is available.)

```bash
# download the software - arduino-nightly-linux64.tar.xz
# from https://www.arduino.cc/en/Main/Software

# uncompress the tarball
cd ~/Downloads
tar -xvf arduino-nightly-linux64.tar.xz

# move the result folder to /opt directory for global use
mv arduino-nightly arduino-Dec-16-2016
sudo mv arduino-Dec-15-2016 ~/src

# run the script to install both desktop shortcut and launcher icon
cd /home/src/arduino-Dec-16-2016
chmod +x install.sh
./install.sh
ln -s ~/src/arduino-Dec-16-2016/arduino ~/bin/arduino

# brltty (braille device) which will conflict with the Arduino
sudo apt-get remove brltty
```

When the Arduino Software IDE is properly installed you can execute
the IDE via the command `arduino &>/dev/null &`.

It might hapen that when you upload a sketch - after you have selected your board and serial port -, you get an error Error opening serial port ... If you get this error, you need to set serial port permission. See - https://www.arduino.cc/en/Guide/Linux

Arduino Project Hub - https://create.arduino.cc/projecthub

Arduino IDE Now Supports Building Software in the Command Line - http://lifehacker.com/arduino-ide-now-supports-building-software-in-the-comma-1740786363

# Installing Arduino Command Line Tools
**NOTE:** Below needs to be updated. See [Arduino Builder](https://github.com/arduino/arduino-builder).
and [Arduino IDE Now Supports Building Software in the Command Line](http://lifehacker.com/arduino-ide-now-supports-building-software-in-the-comma-1740786363).

For someone like myself, who is at home with Linux as my OS and Vim as my editor,
using the Arduino IDE for Arduino coding is a step back into the stone age.
If you are used to doing these things yourself and controlling the organization of your code
then the Arduino IDE does some really arbitrary and annoying things.
For example, try sharing a common file between your sketch and modules (that is, Arduino libraries)
which you may or not use depending on what sketch you are compiling.
The Arduino will compile everything in the directory with the included file.
You have no say in what gets compiled and in what context.

I'm not the first to lament about the this topic, but more importantly, some people
have stepped forward and done something about it!
The folks at Arduino have given us [Installing Arduino on Linux][01], which gives us
a Arduino IDE, but more importantly, the foundation of this package are executables and libraries
that can be called executed outside of the IDE.
Others like [Martin Oldfield and Sudar Muthu][02] have given us the Linux package `arduino-mk`
which allows you to use the core tools that form the foundation for the Arduino IDE.
Those foundational tools are within the package `arduino-core`.
The actual Arduino IDE is in the package `arduino`.

Never the less, there has been some complaints that the package `arduino-mk` doesn't work out of the box.
Martyn Davis has written [this article][03] describing the steps he found necessary
to get Arduino programming up and running from the command line.
I found I didn't have to make the fixes Martyn specified, I assume because the code base has been updated.

In my case, I'm setting up a development environment
using the nRF24L01+ radios on both the Raspberry Pi (RPi) and Arduino.
Basically, I plan to have a RPi as the radio hub with multiple nodes reporting back status.
Those nodes will be other RPi's or some variant of Arduino.
This mixed hardware environment will likely call for common header files,
similar code files but not exactly the same, which can be handed by libraries tailored to the hardware.

I want to have all the code reside on the RPi,
and a super makefile that will build the software for both the RPi and the Arduino.
I want a single instance of code files with hardware dependencies handle via cpp preprocessor variables.
All this is very doable within Linux, but coding for the Arduino with its IDE, will make it impossible.
Using `arduino-mk` should address some of my issues but it wasn't clear how I wll handle libraries.
Here is how made this into a success.

```
sudo apt-get install arduino-core arduino-mk
sudo usermod -a -G dialout pi
```
The `usermod -a -G dialout pi` may not be need if `pi` is already in the group.
You can check via `grep dialout /etc/group`.
If you need to update the group, log out and back in again so the group permissions take effect.

A main makefile is included under /usr/share/arduino/Arduino.mk. It can be used to build an Arduino project by creating a small project specific makefile, refer to the main makefile and finally define a few required constants.

You should then set up environment variables thus:

```
ARDUINO_DIR   = /usr/share/arduino
ARDMK_DIR     = /usr/local
AVR_TOOLS_DIR = /usr
```

You should be able to build an Arduino program using `make` and place the code
below in a file called `Makefile`.
You'll need to adjust the `ARDUINO_LIBS`, `TARGET`, etc. variables to meet your needs.

```
# Where the Arduino software has been unpacked
ARDUINO_DIR = /usr/share/arduino

# The basename used for the final files.
# Canonically this would match the .pde file, but it's not needed here: you could always set it to xx if you wanted!
TARGET = CLItest

# List of any libraries used by the sketch (we assume these are in $(ARDUINO_DIR)/hardware/libraries
# e.g. EEPROM Firmata SD SoftwareSerial Stepper Ethernet Ethernet/utility LiquidCrystal Servo SPI Wire Wire/utility
ARDUINO_LIBS = SPI

# The ard-parse-boards tag for the board.  Execute 'make show_boards' to show a list.
# e.g.  mega mega2560 mini mini328 nano nano328 uno
BOARD_TAG = uno

# The port where the Arduino can be found (only needed when uploading the sketch)
# e.g. /dev/ttyACM*
ARDUINO_PORT = /dev/arduino

# The include directive tells make to suspend reading the current makefile and
# read one or more other makefiles before continuing.
include /usr/share/arduino/Arduino.mk
```

Checkout the example given here for ideas (e.g. MONITOR_PORT = /dev/cu.usb*): https://github.com/sudar/Arduino-Makefile

* [Compiling Arduino sketches using Makefile](http://hardwarefun.com/tutorials/compiling-arduino-sketches-using-makefile)
* [Arduino from the command line](http://blag.pseudoberries.com/post/1036381516/arduino-from-the-command-line)
* [Arduino from the command line](http://www.themgames.net/arduino-from-the-command-line/)
* [Arduino 1.0 development with a makefile on Linux](http://www.itopen.it/2012/02/12/arduino-1-0-development-with-a-makefile/)
* [Build Arduino CLI Environment with Vim](http://arduinoexplained.blogspot.com/2012/10/build-arduino-cli-environment-with-vim.html)
* [Flashing an Arduino from a Raspberry Pi](http://blog.hekkers.net/2013/11/02/flashing-an-arduino-from-a-raspberry-pi/)
* [Arduino sketches on RPi](http://jeelabs.org/2013/01/17/arduino-sketches-on-rpi/)
* [Uploading a sketch from the command-line](http://www.jamesrobertson.eu/blog/2012/sep/20/uploading-a-sketch-from-the-comman.html)
* [Programming and uploading Arduino sketch without IDE](http://www.linuxcircle.com/2013/05/15/programming-and-uploading-arduino-sketch-without-ide/)
* [Uploading Sketches to the Arduino on the Pi](http://www.deanmao.com/2012/08/10/uploading-sketches-to-the-arduino-on-the-pi/)
* [Compiling and uploading arduino programs without the IDE](http://www.vascop.com/compiling-and-uploading-arduino-programs-without-the-ide.html)
* [Advanced Arduino Hacking](http://pragprog.com/magazines/2011-04/advanced-arduino-hacking)

Others
* [Arduino Makefile](http://ed.am/dev/make/arduino-mk)
* [Advanced Arduino – Including Multiple Libraries In Your Project](http://provideyourown.com/2011/advanced-arduino-including-multiple-libraries/)

Files
* http://bisqwit.iki.fi/jutut/kuvat/programming_examples/epromread/Arduino.mk
* http://www.ualberta.ca/~jhoover/web_docs/resources/arduino-ua/mkfiles/Arduino.mk


### Serial Port Monitoring
One of the things that comes free with the Arduino IDE is a serial monitor.
Of course, this is an indispensable tool for both testing and debugging.
But we haven't abanded this capability since there are Linux alternatives.
The post [Arduino and Linux TTY][04] provides a series of solutions.
(What is listed below isn't always functional for every need, so consult the posting for more ideas.)
Assuming the Arduino's USB is plugged into `/dev/ACM0` and the port speed is set to `57600`,
`cu -l /dev/ttyACM0 -s 57600` will get you simple connect.
Entering `~.` will terminate the connection.
For more commands, consult the [`cu` manual page][07].

sudo chgrp dialout /usr/bin/cu

You can use [`screen`][08] to provide a more interactive serial monitor session with an Arduino.

```
stty -F /dev/ttyACM0 cs8 57600 ignbrk -brkint -imaxbel -opost -onlcr -isig -icanon -iexten -echo -echoe -echok -echoctl -echoke noflsh -ixon -crtscts
screen /dev/ttyACM0 57600
```

Make sure the Arduino is plugged in first, otherwise the `stty` will not take.
Also, you need to only issue the `stty` command once for the terminal session.

To get out of a `screen` session (but not kill it), type `Ctrl-a` then `Ctrl-d`.
Doing this will detach you from the screen session which you can later resume by doing `screen -r`.

The command `screen -ls` will list any screen sessions that might be still running.
To terminate any of these sessions, use  `screen -X -S <ID> kill`).
(for example, `screen -X -S 29879.pts-1.desktop kill`).

See [Linux Screen Tutorial and How To][05]
[Screen User's Manual][06] for more information about the power of `screen`.


### Vim Syntax Highlighting
To top this all off, then use this syntax file and get syntax highlighting for Arduino functions in Vim.
https://github.com/sudar/vim-arduino-syntax


### Sources and Inspiration
* [Arduino from the command line](http://www.mjoldfield.com/atelier/2009/02/arduino-cli.html)



[01]:http://playground.arduino.cc/Learning/Linux
[02]:http://www.mjoldfield.com/atelier/2009/02/arduino-cli.html
[03]:http://www.martyndavis.com/?p=335
[04]:http://playground.arduino.cc/Interfacing/LinuxTTY
[05]:http://www.rackaid.com/resources/linux-screen-tutorial-and-how-to/
[06]:http://www.gnu.org/software/screen/manual/screen.html#Overview
[07]:http://linux.die.net/man/1/cu
[08]:http://www.computerhope.com/unix/screen.htm
[09]:https://www.arduino.cc/en/Guide/Linux
[10]:https://www.intorobotics.com/alternatives-standard-arduino-ide-one-choose/
[11]:https://learn.sparkfun.com/tutorials/what-is-an-arduino
[12]:https://www.arduino.cc/en/Main/Software
[13]:
[14]:
[15]:
[16]:
[17]:
[18]:
[19]:
[20]:

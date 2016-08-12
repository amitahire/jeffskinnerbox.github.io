* [WRTnode Wiki](http://linksprite.com/wiki/index.php5?title=WRTnode)
* [WRTnode Wiki](http://wiki.wrtnode.com/index.php?title=Main_Page)
* [WRTnode Wiki](http://wiki.wrtnode.cc/index.php?title=%E9%A6%96%E9%A1%B5/en)

* [Mount an external USB media as root fs on OpenWRT](http://www.rooot.net/en/geek-stuff/openwrt/36-mount-external-usb-root-partition-openwrt.html)
* [OpenWrt as a wifi client](http://www.rooot.net/en/geek-stuff/openwrt/8-openwrt-wifi-client.html)
* [My complete OpenWrt Setup Guide](http://www.jauu.net/2015/03/03/complete-openwrt-guide/)


![WRTnode](http://photos-h.ak.instagram.com/hphotos-ak-xap1/10802493_381146012045023_126183938_n.jpg =100x100 "In early November 2014, I got from Seeed Studio the WRTnode. WRTnode is based on WiFi WiFi Access Point System on a Chip, is an open source development board hardware using the Mediatek MT7620n chip.")
In early November 2014, I got from [Seeed Studio][21] the [WRTnode][22].
WRTnode is based on WiFi Access Point System on a Chip (SoC),
is an open source development board hardware using the [Mediatek][23] [MT7620n chip][24].
The MT7620 router-on-a-chip includes an 802.11n MAC and baseband, a 2.4 GHz WiFi radio,
a 580 MHz [MIPS][37] CPU ([MIPS 24KEc][38]),
a 5-port 10/100 switch and two
[Reduced Gigabit Media Independent Interface (RGMII)][25].
The WRTnode comes pre-installed with [OpenWrt][40] on the MT7620
and contains everything needed to build an access point router from a single chip.

The WRTnode operates at 300Mbps, WiFi antenna integrated into the PCB board,
has pins pre-configured for some of the LED indicators
you would see on a conventional routers,
four-port Ethernet hub, WAN port, some general-purpose GPIO, and serial console input.
In total, there 78 pins GPIO, and from the picture below (take from the [WRTnode Wiki][04]),
we can see the pinout each and every one of them.

![WRTnode Pin Out](/images/WRTnode_pin_out_v0.2.png =570x374 "Pin out for WRTnode board")(http://wiki.wrtnode.com/images/0/0b/Saving3.png)

> **Note:** In this diagram, WRTnode is photographed showing the side where the pins arre soldered,
so when making connections, you must reverse the pinout.

WRTnode isn't the only tiny and inexpensive Linux solution out there.
Just to name a few:

* [VoCore][07] is an open hardware running OpenWrt.
It has WiFi, USB, UART, 20+ GPIOs but size is only one square inch.
* The [Onion Omega][44] is an ultra small OpenWrt, WiFi development board designed specifically for wireless IoT applications.
* [Linino][64] is based on OpenWrt and is a software framework and operating system
able to integrate _microcontroller_ features inside the _microprocessor_ environment.
You can simply write your application using Node.js, Python, Bash, etc.,
on linux side using LininoOS to control completely the board and all the devices attached.
* My favorate is a hackable product, the [GL-AR150-ext smart router][45].
It has good [documentation][46] and even a [blog][47] for the hacker community.

# Components that Make Up WRTnode
WRTnode is a high performance CPU, low power consuming, cheap,
and small development board that can run OpenWRT, and  therefore,
also easy to port open source software of Linux.

## WRTnode Hardware
![wrtnode](http://www.cnx-software.com/wp-content/uploads/2014/09/WRTnode_large.jpg)
With a built-in [Mediatek MT7620n][75] chip,
WRTnode is an open source development board hardware based on WiFi AP System on a Chip (SOC).
WRTnode is mini, cheap and has pretty low power consumption
and reasonable capability of computing, and capable of high speed of WiFi network exchange.
WRTnode claims its aim is to be a high speed and digital version of "Arduino".
Since it could connect and interact with USB devices like camera and sound card,
you can collect images and voice at the same time and stream out multimedia in real time.
After a layer of A/D converter, it could directly interact with all kinds of sensors and motors.

For more on the WRTnode hardware, check out [this wiki][74].

################################################################################
Replace this with a referance to getting-started-with-openwrt.md

## OpenWrt
[OpenWrt][40] is a descendant of the firmware used for the classic [Linksys WRT54G][39] router.
In fact, this classic Linksys series of routers lead to [DD-WRT][41], [OpenWrt][40], [Tomato][42],
and countless other open-source firmwares.
Read "[The Open Source WRT54G Story][43]" if you want more of a history lesson.

OpenWrt is described as a Linux distribution for embedded devices,
and primarily used on embedded devices to route network traffic.
Like other Linux distributions,
it offers a built-in package manager that allows you to install packages from a software repository.
It can be used for anything that an embedded Linux system can be used for,
including functioning as an SSH server, VPN, or [traffic-shaping][26] router.

Most people will be happy with their router’s default firmware,
while many power users will want a drop-in replacement firmware like [DD-WRT][27].
OpenWrt is more flexible – it’s basically an embedded Linux distribution that
can be installed on various routers.

The main components are:

* [Linux kernel][15] - manages input/output requests from software,
and translates them into data processing instructions the CPU
* [util-linux][13] - standard package of the Linux operating system
* [uClibc][14] - small C standard library intended for Linux kernel-based operating systems
* [BusyBox][16] - software that provides several stripped-down Unix tools in a single executable file
* [Wireless Utilities][68] - utilities for WiFi spcific to the WRTnode implementation of OpenWrt

OpenWrt provides a fully writable filesystem with package management,
allowing you to [customize the device][17] through the use of packages to suit any application.
Also OpenWrt supports a framework to build an application without having to
build a complete firmware around it and is fully customizable.

Another component, but not considered part of OpenWrt, is the [bootloader][48].
The Bootloader is a piece of software that is executed every time the hardware device is powered up.
It is executable machine code, and quite heavily device-specific.
Its main task is to initialize all the low-level hardware details.
The bootloader is commonly on flash storage.

Unlike other router softwatre like DD-WRT,
OpenWrt is completely command line based.
The standard OpenWrt distribution package doesn't include a GUI,
but you can install one called the OpenWrt Configuration Interface, [LuCI][65].

OpenWRT also supports quite a number of hardware platfroms for routers.
You can check whether your particular model is supported
by reviewing the [OpenWrt's hardware table][66].
OpenWRT also supports many security features that you might find useful,
including a firewall based on ipchains, WiFi Protected Access (WPA) encryption,
Remote Authentication Dial-In User Service (RADIUS) authentication,
Dropbear Secure Shell (SSH) server, OpenVPN, amonug others.

### Linux Kernel
There are so many Linux distributions out in the wild,
but there is only one de facto thing that they have in common:
the [Linux kernel][57].
[So what is a kernel][59]?
It’s the kernel that does the grunt work of the operating system.
The kernel’s job is to talk to the hardware and software,
and to manage the system’s resources as best as possible.
It talks to the hardware, via the drivers,
when applications submit there request to the kernel.
The kernel make sure that there is enough memory available for an application to run,
as well as to place an application in the right location in memory
The kernel coordinate these and many other things.
This kernel circus act is [illustrated here][58]
and the Linux kernel [anatomy here][60].

With just a kernel, it’s nearly impossible to do anything with the operating system.
You also need some additional applications/utilities to be bundled with it.
These utilities use the kernel's [system calls][62] to perform useful task,
and a [shell][63] for user interaction.
These additional application  include util-linux, uClibc, and BusyBox discussed below.

### util-linux
util-linux is a standard package of the Linux operating system.
The [util-linux code repository][55] is used by all variants of Linux.
This package contains a number of important utilities,
most of which are oriented towards maintenance of your Linux system.
Some of the more important utilities included in this package allow
you to partition your hard disk, view kernel messages, and create new filesystems.
These utilities are not the every day utilities like vim, grep, cat, etc.
(see Busybox for these)
but instead are operating system utilities.
See [this page][56] for a listing of the utilities within util-linux.

util-linux doesn't contain everything you need for
administering your Linux.
For example, utilities to manage the WiFi on the WRTnode will not be within util-linux.

### uClibc
[uClibc][51] is a small C standard library intended for Linux kernel-based
operating systems for embedded systems and mobile devices.
uClibc is to provide as much functionality as possible in a small amount of space.
uClibc is much smaller than [glibc (GNU C Library)][61]
which is normally used with Linux distributions.
uClibc is specifically focused on embedded Linux and
features can be enabled or disabled according to space requirements.

If you choose to compile programs with uClibc,
you'll to have your own uClibc toolchain. A toolchain consists of
[GNU binutils][52], the [gcc compiler][53], and uClibc,
all built to produce binaries for your target system linked with uClibc.
You can build your own native uClibc toolchain using the [uClibc buildroot system][54].

### BusyBox
[BusyBox][11] is a tool loaded into the OpenWrt environment.
BusyBox combines tiny versions of many common UNIX utilities into a single small executable.
It provides minimalist replacements for most of the utilities you usually find
in GNU fileutils, shellutils, includes [`vi`][12], etc.
BusyBox is extremely configurable, allowing you to include only the components you need.
The utilities in BusyBox generally have fewer options than their full-featured GNU cousins;
however, the options that are included provide the expected functionality
and behave very much like their GNU counterparts.

BusyBox is extremely modular so you can easily include or exclude commands
(or features) at compile time.
This makes it easy to customize your embedded systems.
To create a working system, just add some device nodes in `/dev`,
a few configuration files in `/etc`, and a Linux kernel.

For a listing of Busybox's utilities, check out the [Busybox Manual Page][28].
[BusyBox is a multi-call binary][12], that is,
a single binary acts like a large number of utilities.
BusyBox has built-in utility programs (called applets)
can share code for many common operations.
So it has the following syntax:

```bush
busybox <applet> [arguments...]  # or

<applet> [arguments...]          # if symlinked

Where the applets would include ls, awk, sed, wc, ....
and many other of your favorate Linux commands
```

### WiFi Utilities
Like in standard Linux, WiFi support, wireless in general,
is fragmented.
Wireless devices have an API different from that of Ethernet devices
because the specifications of IEEE 802.11 covers the whole communications process.
The available of some tools depend entirely on your drivers writen for the hardware.
[Tools available through OpenWrt][71], and therfore, support most hardware platforms,
including WRTnode, are:

* `iwconfig` - is the configuration utility for the now obsolete [Wireless-Extensions (WEXT) API][69],
which is scheduled for removal.
* `iw` - is the configuration utility replacing `iwconfig` supporting the [nl80211 API][70].
* `iwinfo` - is a frontend to the custom library, which assembles information from various places.
* `hostapd` - this package contains a full featured IEEE 802.1x/WPA/EAP/RADIUS Authenticator.
* `wpa-cli` -  this is a WPA Supplicant command line interface

Beyond what utilities OpenWrt povides for WiFi,
WRTnode comes with some [custom utilities][68] (`aps`/`setwifi`/`ia`/`vw`/`nr`/`wifi`)
for the up-link part of the router inside of WRTnode.

* `aps` - is a WRTnode customized command which scans the WiFi SSIDs available.
* `vw` - is used to make changes to `/etc/config/wireless` where WiFi configuration information is stored, using the file editor `vi`.
* `nr` - is a WRTnode customized command which will reset the network side.  After 5 seconds it is possible to connect again to WRTnode's SSID.
* `ia` - is the WRTnode equivalent to `ifconfig`, the Linux network interface configuration, control, and query tool.
* `wifi` -  is a WRTnode customized command which will reset the network side. After 10 seconds it is possible to connect again to WRTnode's SSID.
* `setwifi` - is used to connect to an access point when give its SSID and password

[OpenWrt also support many WiFi modes][72] such as AP, Monitor, Ad-Hoc, [802.11s][73], and more.

### Bootloader
The WRTnode incldues a customized [uboot][29] which is a popular [bootloader][30] that
supports multiple architectures (ARM, MIPS, AVR32, Nios, Microblaze, 68K and x86)
and filesystems (FAT32, ext2, ext3, ext4 and Cramfs).

Strictly speaking, a bootloader is not required to boot Linux.
The use of one (or several) bootloaders in a row to chainload (or [bootstrap][49])
a Kernel is not a categorical necessity,
but it is a preferred method to start an operating system.
The main advantage for OpenWrt is,
that the existence of a bootloader offers users and developers
additional possibilities to [debrick][50] a device.

################################################################################

# Getting Connected with WRTnode
Read the [OpenWrt New Comer's Guide][67]

## Getting Connected with WRTnode Via WiFi
The easiest way to get connected with WRTnode/OpenWrt on Ubuntu is via
the [network menu in the menu bar][08].
We know from the [WRTnode documentation][04]
that the SSID being broadcasted by the WRTnode is "WRTnodeXXXX",
where the XXX is the last 4 digits of the OpenWrt's MAC address.
In my case its "WRTnode9976".
The [WRTnode documentation][04] also says that the default WiFi password is "12345678".

To get this to work successfully, I had to turn off my Ethernet connection.
It appears that the DHCP server via the Ethernet and via the WRTnode were
not playing well together.
Even with Ethernet turned off, in time,
my connection to the WRTnode would slow down and then freeze.
My guess is that Ubuntu has some WiFi management daemons running
that is getting in the way.
If I had a separate laptop or other WiFi enabled computer,
I could have been successful.

## Getting Connected with WRTnode Via Serial Console
We do have an alternative to WiFi connectivity to WRTnode,
that is, via the serial console port on the WRTnode board,
and thus access via a terminal.
This can be very useful, allowing you to access WRTnode as root,
without entering the password.
I will make this console connection using an [Adafruit FTDI Friend][32]
(make sure to modify the jumper setting on the back for 3.3V logic and 3.3V VCC).
This will allow me to connect my Linux box to the WRTnode via a USB port and a terminal emulator.

### Make the USB Device Persistent
The first thing I want to do is make this USB device have a [persistent device name][36].
If this isn't done, the Linux kernel will automatically assign it a device name
and you need to dance around to find the device.
The first step in getting this solved is to the following:

```bash
# find out what device the FTDI Friend has been assigned to
$ lsusb | grep Future
Bus 001 Device 019: ID 0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART) IC
```

This tells us the Bus FTDI Friend's VendorID:ProductID pair is `0403:6001`.
This also tells us that the FTDI Friend has been assigned to bus 001 and device 014,
which translate to the device `/dev/bus/usb/001/019`.
No using `udevadm` command, you get the final piece of information required:

```bash
# get the serial number for of the device
$ udevadm info -a -n /dev/bus/usb/001/019 | grep ATTR{serial}
    ATTR{serial}=="A501E3BN"
```

So now you know the serial number of the FTDI Friend you own is `A501E3BN`.
Armed with this information and following guidance from [this post][34], I can now update the [UDEV rules][35].
I'll create a UDEV rule set that’ll make a symbolic link, called `/dev/ftdifriend`, for the FDTI Friend.
UDEV rules are located in the `/etc/udev/rules.d` directory.
I'll create a new file called `jeffs.rules` within the `udev` rules directory
and put in the following line:

```
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="A501E3BN", SYMLINK+="ftdifriend"
```

Now unplug and then plug back in the FDTI Friend.
If you do `ls -l /dev/ftdifriend`
you'll see the device and its symbolic link.
No more USB port dancing to find the FDTI Friend!

### Pin Connections to Access Console
[This web post][33] will provide some insight on
what pins to connect to on the WRTnode and access the console via the FTDI Friend.
My diagram for pin connections are given below:

![console pins](/home/jeff/Downloads/junk.jpg "Pin connections to access the OpenWrt console and pwer the board")

>**Note: The FTDI Friend will not power the WRTnode.
You still have to supply power via the micro USB plug.

To test if the FDTI Friend console assess is working,
use `microcom -p /dev/ftdifriend` and you should
now have access to console without any password.
It should be very responsive and you will not be clashing with
your Linux boxes attempt to manage WiFi, as referenced earlier.

# First Time Login to OpenWrt (via WiFi)
The [first time you connect to OpenWrt][01] via WiFi,
(none of this applies to login via console),
you will do so via `telnet` in order to set the root password and start using `ssh`.

```bash
# telnet into OpenWrt without a password
telnet 192.168.8.1
.
.
.
# change the root password.  This will also turn off telnet and you can now use ssh to log in
passwd
```

At this point, you must use `ssh` to login with your new password

```bash
# secure login into OpenWrt
ssh root@192.168.8.1
```

OpenWrt also supports a web user interface, called [LuCI][18],
accessible via a browser via URL `192.168.8.1`.
You'll login as root using the password created for the establishment of `ssh`.

# WRTnode Commands and Helpful Tools
These commands are part of Busybox or OpenWrt,
and can be very useful:

* BusyBox box version - `busybox | head -1`
* Linux kernel version - `uname -r` or `dmesg | grep Linux`
* OpenWrt version - `cat /etc/banner`
* syslog messages - `logread`
* kernel messages - `dmesg`
* OpenWrt packages installed - `opkg list`, see [OpenWrt documentation][03] for more commands
* BusyBox commands - `help` provides a list of supported applets

![openwrt help command](/images/openwrt-help-command.jpg "BusyBox commands support on OpenWrt")

A symbolically linked command is the `ls` command.
Using this, you can exploit the file system to see some of the contents of OpenWrt.

![openwrt bin dir](/images/openwrt-file-system.jpg "Some of OpenWrt's filesystem")

check out http://wiki.openwrt.org/doc/howto/snippets

## Scanning for Other Access Points
`aps` is a WRTnode customized command which scans for the WiFi SSIDs available.
Scan for Access Points that WRTnode's can reach.

```bash
root@OpenWrt:~# aps
WRTnode AP scaner.
Begin scaning APs, pls wait...
Finished.
APs available are...
ra0       get_site_survey:
Ch  SSID                             BSSID               Security               Siganl(%)W-Mode  ExtCH  NT WPS DPID
1   TRENDnet637                      00:14:d1:c3:c0:6f   WEP                    29       11b/g/n NONE   In YES
6   Download Virus                   90:72:40:1b:c4:c6   WPA2PSK/AES            29       11b/g/n NONE   In  NO
6   F9MH4                            00:26:62:73:0e:f8   WEP                    44       11b/g/n NONE   In  NO
6   Battlestar                       00:26:62:66:92:3f   WPA1PSKWPA2PSK/AES     5        11b/g/n NONE   In  NO
6   7D6GC                            00:26:b8:65:a6:e5   WEP                    24       11b/g/n NONE   In  NO
6   74LL5                            00:1f:90:b4:8a:80   WPA1PSKWPA2PSK/AES     100      11b/g   NONE   In  NO
6   W7JKF                            f8:e4:fb:7c:7a:b1   WPA2PSK/AES            10       11b/g/n NONE   In  NO
6   Bridge-2.4                       e8:fc:af:93:b8:f9   WPA1PSKWPA2PSK/TKIPAES 86       11b/g/n NONE   In YES
6   Guest Network                    92:c6:c4:1b:40:70   WPA2PSK/AES            39       11b/g/n NONE   In  NO
11  CRL-EmployeesOnly                9c:1c:12:3e:c8:e0   WPA2/AES               10       11b/g/n NONE   In  NO
11  NETGEAR99                        10:0d:7f:8b:ce:3f   WPA2PSK/AES            15       11b/g/n NONE   In YES
11  RFOS8                            00:18:01:e3:08:ee   WEP                    20       11b/g   NONE   In  NO
11  Campbell-WLAN                    00:1f:90:fb:27:20   WPAPSK/TKIP            5        11b/g   NONE   In  NO
```

## Connecting with the Internet
To connect to the Internet,
WRTnode must configuring the up-link part of the router inside of WRTnode.
This is equivalent to the Ethernet WAN interface of your home router,
except your going to connect to your home WiFi router, which is your gateway to the Internet.
The WRTnode wiki article, [No internet no happiness][20], give you the details
need to do this.

Change the settings of `aplci` on WRTnode.
`aplci` is the up-link part of the router inside of WRTnode.
To see how things a initially configured,
run the `ia` command, WRTnode equivalent to `ifconfig`:

```bash
root@OpenWrt:~# ia
apcli0    Link encap:Ethernet  HWaddr 66:51:7E:32:99:76
          inet6 addr: fe80::6451:7eff:fe32:9976/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```

To establish connection to the Internet via your home router,
make the changes via the WRTnode customized command `vw` which changes `/etc/config/wireless`.
It is used the file editor `vi`.

```bash
root@OpenWrt:~# vw

<screen refresh>

config wifi-device 'ra0'
        option type 'ralink'
        option mode '9'
        option channel '6'
        option txpower '100'
        option ht '20+40'
        option country 'US'
        option disabled '0'

config wifi-iface
        option device 'ra0'
        option network 'lan'
        option mode 'ap'
        option encryption 'psk2'
        option key '12345678'
        option ApCliEnable '1'
        option ApCliSsid 'aAP'
        option ApCliAuthMode 'WPA2PSK'
        option ApCliEncrypType 'AES'
        option ApCliPassWord '87654321'
        option ssid 'WRTnode9976'
```

...Use hightlight to illustrate what values need to be changed...

```
config wifi-device 'ra0'
        option type 'ralink'
        option mode '9'
        option channel '6'
        option txpower '100'
        option ht '20+40'
        option country 'US'
        option disabled '0'

config wifi-iface
        option device 'ra0'
        option network 'lan'
        option mode 'ap'
        option encryption 'psk2'
        option key '12345678'
        option ApCliEnable '1'
        option ApCliSsid 'aAP'
        option ApCliAuthMode 'WPA2PSK'
        option ApCliEncrypType 'AES'
        option ApCliPassWord '87654321'
        option ssid 'WRTnode9976'
```

Next you need to rest the network.
`nr` is a WRTnode customized command which will reset the network side.
After 5 seconds it is possible to connect again to WRTnode's SSID.

```bash
root@OpenWrt:~# nr
```

Now verify if WRTnode got an IP from from your home WiFi Access point
by using the `ia` command, WRTnode equivalent to `ifconfig`:

```bash
root@OpenWrt:~# ia

...get listing

```

Finally, verify if WRTnode is connected to Internet.

```bash
root@OpenWrt:~# ping www.google.com

...get listing

```

So now the WRTnode board is connected to the Internet through our home router.
You can connect to the Internet start configure our WRTnode board.

## Helpful Tools
As I begain to play with the WRTnode, I ran into several problems,
most of my own making.
To monitor what is going on with the WRTnode, I found the following tools useful

* Tools for Monitoring WiFi
    * [`wavemon`][02] is a ncurses-based monitoring application for wireless network devices.
    It displays continuously updated information about signal levels, as well as,
    wireless-specific and general network information.
    **Example Usage:** `wavemon wlan0`
    * [`iwevent`][05] is another command line tool that displays wireless events
    received through the [RTNetlink socket][06].
    Each line displays the specific wireless event which describes
    what has happened on the specified wireless interface.
    **Example Usage:** `iwevent`
* Tools for Monitoring NIC
    * [`netstat`][10] (network statistics) is a command-line tool that displays
    network connections for TCP (both incoming and outgoing),
    routing tables, and a number of network interface and network protocol statistics.
    **Example Usage:** `netstat -ie`
    * [`nicstat`][09] prints network traffic, packets or Kb/s read and written.
    Its a utility like `top` for network interface card (NIC).
    It displays information and statistics about all your network card such as packets,
    kilobytes per second, average packet sizes and more.
    **Example Usage:** `nicstat -i wlan0 1`
* OpenWrt Console Connection
    * [`telnet`][31] is a protocol which is part of the TCP/IP suite and used on the
    Internet or local area networks to provide a bidirectional interactive
    text-oriented communication facility using a virtual terminal connection.
    **Example Usage:** `telnet 192.168.8.1`
# Other Things
So now that your logged into the WRTnode, now what?
The [WRTnode Wiki][19] does give some good ideas.
For starters, your going to want to connect with the Internet to load OpenWrt packages,
update firmware, etc.

## Update OpenWrt Software Repository
http://wiki.wrtnode.com/index.php?title=Starting#WRTnode_software_repository

## Restore Factory Settings
http://wiki.wrtnode.com/index.php?title=Starting#Restore_Factory_Settings

## More
http://wiki.wrtnode.com/index.php?title=Main_Page
[The Pain of Connecting to WPA Wi-Fi on the Linux Command Line](http://www.sevenforge.com/2009/07/28/connecting-to-wpa-wifi-on-the-command-line/)
[NetworkConfigurationCommandLine/Automatic](https://help.ubuntu.com/community/NetworkConfigurationCommandLine/Automatic)
[OpenWrt Debricking Guide](http://wiki.openwrt.org/doc/howto/generic.debrick)
[FAQ after Installation of OpenWrt](http://wiki.openwrt.org/doc/faq/after.installation)

####################
`ping` (Packet Internet Gropper)

`telnet` (teletype network) is a network protocol used on IP networks to provide a bidirectional
interactive text-oriented communication facility using a virtual terminal connection.

`route` manipulates the kernel's IP routing tables.

`ifconfig` is  used to configure the kernel-resident network interfaces.
It is used at boot time to set up interfaces as necessary.

`arp` (address resolution protocol) is used to translate protocol addresses to
hardware interface addresses.
The arp command displays a table of translated hardware addresses in the cache.


####################


# WRTnode
* [WRTnode](http://wrtnode.com/w/)
* [wrthelp – a demo app for the WRTnode](http://blog.thestateofme.com/2014/09/21/wrthelp/)
* [Getting Started with WRTnode OpenWrt Development Board](http://www.cnx-software.com/2014/09/18/wrtnode-quick-start-guide/)
* [WRTnode Wiki](http://wiki.wrtnode.com/index.php?title=Main_Page)
    * [WRTnode Getting Started Guide](http://wiki.wrtnode.com/index.php?title=Starting)
    * [Refresh the Firmware](http://wiki.wrtnode.com/index.php?title=Refresh_the_firmware)
* [Become your own router with WRTNode - Controlling WRTNode through the serial console](http://www.peatonet.com/en/hazte-tu-propio-router-con-wrtnode-controlando-wrtnode-a-traves-del-puerto-serie-de-consola/)
* [Become your own router with WRTNode - Adding four LAN ports and one WAN port](http://www.peatonet.com/en/hazte-tu-propio-router-con-wrtnode-anadiendo-cuatro-puertos-lan-y-un-puerto-wan/)

* [Part 1 - Introduction to WRTNode what is it how to find info](https://www.youtube.com/watch?v=KGdhDl_uNz0)
* [Part 2 - WRTnode how to connect and connect it to your network](https://www.youtube.com/watch?v=0wG2lg5omz8)
* [Part 3 - WRTnode setup firewall to allow access from home network](https://www.youtube.com/watch?v=3az3SupnbhI)
* [Part 4 - WRTnode setup usb camera and mjpg streamer](https://www.youtube.com/watch?v=HyCm2RXRB4E)
* [WRTNode Playlist](https://www.youtube.com/playlist?list=PLrIDWbyydDJA6Nsva4Btflg9WWlABO6u_)

* [Finding a device IP Address](http://www.cnx-software.com/2010/10/25/finding-a-device-ip-address/)

# Broadband-Hamnet / HSMM-MESH
[Broadband-Hamnet][02] (formerly called HSMM-Mesh) is a high speed, self discovering,
self configuring, fault tolerant,
wireless computer network that can run for days from a fully charged car battery,
or indefinitely with the addition of a modest solar array or other supplemental power source.
The focus is on emergency communications.
In its current form it is built using the Linksys WRT54G/GL/GS wireless routers
and operates on channels 1-6 of the 2.4GHz ISM band,
which overlaps with the upper portion of the 13cm amateur radio band.
Other platforms and bands are in development at this time.
Next will be Ubiquiti equipment with others supported as development resources permit.

* [1. Introduction To HSMM-MESH Or Broadband-Hamnet]()
* [2. Setting up a MESH Node for Amateur Radio - WRT54G firmware install](https://www.youtube.com/watch?v=pryc8jIl6Xo)
* [3. HSMM-MESH Update Firmware on a Remote Node](https://www.youtube.com/watch?v=vvFjK-Ihk9c)
* [Cheat Sheet – HSMM](http://www.hdecommgrp.org/?p=223)
* [Griff's Digital Ham Radio Site](http://w5vwp.com/index.shtml)



[01]:http://wiki.openwrt.org/doc/howto/firstlogin
[02]:http://www.raspberrypi-spy.co.uk/2014/10/how-to-use-wavemon-to-monitor-your-wifi-connection/
[03]:http://wiki.openwrt.org/doc/techref/opkg
[04]:http://wiki.wrtnode.com/index.php?title=Starting
[05]:http://linux.about.com/library/cmd/blcmdl8_iwevent.htm
[06]:http://www.linuxjournal.com/article/8498
[07]:http://hackaday.com/2015/11/15/vocore-tutorial-gets-you-started-with-tiny-router/
[08]:https://help.ubuntu.com/14.04/ubuntu-help/net-wireless-connect.html
[09]:http://www.cyberciti.biz/hardware/linux-install-nicstat-command-to-print-network-statistics-for-nics/
[10]:http://www.binarytides.com/linux-netstat-command-examples/
[11]:http://www.busybox.net/
[12]:http://en.wikibooks.org/wiki/Learning_the_vi_Editor/BusyBox_vi
[13]:http://en.wikipedia.org/wiki/Util-linux
[14]:http://en.wikipedia.org/wiki/UClibc
[15]:http://en.wikipedia.org/wiki/Linux_kernel
[16]:http://en.wikipedia.org/wiki/BusyBox
[17]:http://www.makeuseof.com/tag/what-is-openwrt-and-why-should-i-use-it-for-my-router/
[18]:http://wiki.openwrt.org/doc/howto/firstlogin#luci
[19]:http://wiki.wrtnode.com/index.php?title=Starting
[20]:http://wiki.wrtnode.com/index.php?title=Starting#No_internet_no_happiness
[21]:http://www.seeedstudio.com
[22]:http://wrtnode.com/w/
[23]:http://www.mtk.com.tw/en/news-events/mediatek-news/mediatek-first-to-bring-80211ac-1t1r/
[24]:http://www.anz.ru/files/mediatek/MT7620_Datasheet.pdf
[25]:http://en.wikipedia.org/wiki/Media_Independent_Interface#Reduced_Media_Independent_Interface
[26]:http://en.wikipedia.org/wiki/Traffic_shaping
[27]:http://en.wikipedia.org/wiki/DD-WRT
[28]:http://linux.die.net/man/1/busybox
[29]:http://www.linuxjournal.com/content/handy-u-boot-trick
[30]:http://www.addictivetips.com/mobile/what-is-bootloader-and-how-to-unlock-bootloader-on-android-phones-complete-guide/
[31]:http://linux.die.net/man/1/telnet
[32]:https://www.adafruit.com/products/284
[33]:http://www.peatonet.com/en/hazte-tu-propio-router-con-wrtnode-controlando-wrtnode-a-traves-del-puerto-serie-de-consola/
[34]:http://hackaday.com/2009/09/18/how-to-write-udev-rules/
[35]:http://wiki.debian.org/udev
[36]:http://hintshop.ludvig.co.nz/show/persistent-names-usb-serial-devices/
[37]:http://en.wikipedia.org/wiki/MIPS_instruction_set
[38]:http://www.systemc-cpu-models.org/mips_models/24kec/
[39]:http://en.wikipedia.org/wiki/Linksys_WRT54G_series
[40]:https://openwrt.org/
[41]:http://www.dd-wrt.com/site/index
[42]:http://www.polarcloud.com/tomato
[43]:http://www.wi-fiplanet.com/tutorials/article.php/3562391
[44]:https://onion.io
[45]:http://www.amazon.com/GL-AR150-ext-External-Antenna-150Mbps-Pre-installed/dp/B015CYI8DY/ref=sr_1_2?ie=UTF8&qid=1454383159&sr=8-2&keywords=GL-AR150
[46]:http://www.gl-inet.com/docs/wiki/#!index.md
[47]:http://www.gl-inet.com/blog/
[48]:https://en.wikipedia.org/wiki/Booting#BOOT-LOADER
[49]:https://en.wikipedia.org/wiki/Bootstrapping#Computing
[50]:https://wiki.openwrt.org/doc/howto/generic.debrick
[51]:https://www.uclibc.org/
[52]:https://sourceware.org/binutils/
[53]:https://gcc.gnu.org/
[54]:https://buildroot.org/
[55]:https://git.kernel.org/cgit/utils/util-linux/util-linux.git/
[56]:http://www.linuxfromscratch.org/lfs/view/development/chapter06/util-linux.html
[57]:https://kernel.org/
[58]:http://www.makelinux.net/kernel_map/
[59]:http://www.howtogeek.com/howto/31632/what-is-the-linux-kernel-and-what-does-it-do/
[60]:http://www.ibm.com/developerworks/library/l-linux-kernel/
[61]:https://en.wikipedia.org/wiki/GNU_C_Library
[62]:https://en.wikipedia.org/wiki/System_call
[63]:https://en.wikipedia.org/wiki/Shell_(computing)
[64]:http://www.linino.org
[65]:https://wiki.openwrt.org/doc/howto/luci.essentials
[66]:https://wiki.openwrt.org/toh/views/toh_extended_all
[67]:https://wiki.openwrt.org/doc/playground/newcomer
[68]:http://wiki.wrtnode.cc/index.php?title=%E5%A6%82%E4%BD%95%E9%80%9A%E8%BF%87%E6%97%A0%E7%BA%BF%E8%BF%9E%E4%B8%8A%E4%BA%92%E8%81%94%E7%BD%91/en
[69]:http://linuxwireless.org/en/developers/Documentation/Wireless-Extensions/
[70]:http://linuxwireless.org/en/developers/Documentation/nl80211/
[71]:https://wiki.openwrt.org/doc/howto/wireless.utilities
[72]:https://wiki.openwrt.org/doc/techref/wireless.modes
[73]:https://wiki.openwrt.org/doc/howto/mesh.80211s
[74]:http://wiki.wrtnode.com/index.php?title=Main_Page
[75]:https://www.anz.ru/files/mediatek/MT7620_Datasheet.pdf
[76]:
[77]:
[78]:
[79]:
[80]:

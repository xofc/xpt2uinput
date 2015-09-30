# xpt2uinput
User mode driver for Raspberry Pi's 5 inch 800x480 HDMI/P1 with XPT2046 resistive touchscreen controller

This short (kind of) experimental driver reads XY pos and touch state
though the SPI bus (on the connector P1 of Raspberries) and sends events
to /dev/uinput.  It is to be used with WaveShare 5 Inch HDMI LCD with a P1 connector.

Wiring :
* P1-19 SPI MOSI
* P1-21 SPI MISO
* P1-22 Pen IRQ GPIO low when screen is 'touched'
* P1-23 SPI clock (mode 0)
* P1-26 CS1 Chip Select

Relevant documents :
* http://www.waveshare.com/5inch-hdmi-lcd.htm
* https://ldm-systems.ru/f/doc/catalog/HY-TFT-2,8/XPT2046.pdf XPT2046 datasheet
* http://www.airspayce.com/mikem/bcm2835/ BCM2835 C library
* http://ipsolutionscorp.com/raspberry-pi-spi-utility/ (SPI programming example)
* https://github.com/MatthewLowden/RPi-XPT2046-Touchscreen-Python (XPT2046 example)
* http://chipotons.blogspot.be/2015/09/52pis-5-inch-hdmi-touch-screen.html (hacking)
* https://github.com/derekhe/wavesahre-7inch-touchscreen-driver (/dev/uinput example)

usage : 'sudo ./xpt2uinput

Notes :
* The calibration is hardwired...
* Mouse emulation with relative events should probably be more appropriate

HDMI setup in /boot/config.txt
<pre>
#increase HDMI signal strength (just a black screen if not set!)
config_hdmi_boost=4

#remove black borders
disable_overscan=1

#set specific CVT mode
hdmi_cvt 800 480 60 6 0 0 0

#set CVT as default
hdmi_group=2
hdmi_mode=87
</pre>

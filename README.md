# 2019 Easy Bee Counter

This version of the bee counter is all through hole components.  I really wanted to make an easy to assemble bee counter for folks just starting out. I haven't tested this yet but I wanted to get it out early with a few improvements.  The code is pretty simple and I'll post it as soon as I can test it with bees flying this srping.

I've posted two versions. One with an [Adafruit Itsy-bitsy](https://www.adafruit.com/product/3727) uController and one with an [Adafruit Feather](https://www.adafruit.com/product/3405) footprint. The ItsyBitys features a SAMD21 32bit uController.  Adafruit has a ton of options for [Feathers](https://www.adafruit.com/feather?gclid=CjwKCAiA__HvBRACEiwAbViuU4KmYZReV6xjxJxF3YukMTgs1Nm24d_llHE2fEjVRg_X098fisb-hBoCh80QAvD_BwE) but I thought that the wifi esp32, esp8266, or LoRA might be great options.

All the other componets are similar between the two PCB versions.  Powered by 5V.

### Major Differences/Improvments
- All through-hole components for easy soldering
- A total of 24 gates, 48 sensors, 6 shift registers
- ~14.75" long stretching the entire opening of a langstroth hive for easy placement
![gerber-long](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/gerber_itsy_2.PNG)
- Socketed off the shelf uControllers for quick setup. Adafruit ItsyBitsy or Feather
![itsy](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/gerber_itsy_1.PNG)
Feather Footprint. Choose your flavor.
![feather](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/gerber_feather_1.PNG)
- using 2 PCBs to create a sandwich. This is an inexpensive solution and makes for a tight package. The PCBs must be ordered [black](https://github.com/hydronics2/2019-easy-bee-counter/tree/master/instructions/ordering_instructions) so the IR LEDs/sensors work well.

![pic](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/pcb_notes_.PNG)
- using 6 pin headers as dividers and spacers to create gates
- N-Ch mosfet controlled IR LEDs such that LEDs can be controlled ON for short periods during while sensing (~20us). This is a modest enregy savings feature but seems prudent given that turning all LEDs on can pull almost 1/2 amp!


### General Operation
Honeybees are forced through 24 gates where optical sensors (2 per gate) sense whether the bee is present and determine the direction of the bee movement.  Each optical sensors has an IR LED and an IR sensor. If no bee is present the IR light is abosorbed into the black surface. If a bee is present the IR light reflects off the bee back into the sensor. ![https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/IR_photo_diode.PNG](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/IR_photo_diode.PNG)

### uController Pinout
#### ItsyBitsy Pinout
![itsy](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/itsy_pinout.PNG)
#### Feather Pinout
![feather](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/feather_pinout.PNG)

### Shift-in registers
There are 6 shift-in registers. Here's a great description for how to connect and program [shift registers](http://www.gammon.com.au/forum/?id=11979).  The uController's SPI pins read the shift registers. Gates 1-12 are connected to the first 3 shift registers and gates 13-24 the next 3 shift registers. Pulling the chip select pin low enables each bank of shift registers. The sensors are normally pulled low and show 3.3V or HIGH when a bee is present.

### IR LEDs
There are 48 reflective sensors and each IR sensor has an IR LED. They are divided into two sets of 24 with each set controlled by an N-ch mosfet.  The forward voltage of each IR LED is 1.2V and about 20ma as shown on the [data sheet](https://www.sparkfun.com/datasheets/Robotics/QR_QRE1113.GR.pdf). Two LEDs are connected in series with a 22ohm resistor. 
![led schematic](https://github.com/hydronics2/2019-easy-bee-counter/blob/master/pics/led_schematic.PNG)


### Bill of Materials
#### uController
- itsyBitsy M0 32bit SAMD from [mouser](https://www.mouser.com/ProductDetail/485-3727)
- feather Huzzah from [mouser](https://www.mouser.com/ProductDetail/485-3591)
- feather esp8266 from [mouser](https://www.mouser.com/ProductDetail/485-2821)
- feather LoRa 900mhz from [mouser](https://www.mouser.com/ProductDetail/485-3178)
#### PCB
[JLCPCB](https://jlcpcb.com/quote#/) ~$16-25 with shipping. Order the PCBs Black. See [these instructions](https://github.com/hydronics2/2019-easy-bee-counter/tree/master/instructions/ordering_instructions) for ordering.
#### Parts and Pieces from [mouser](https://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=054286973a)
- [qre1113 Reflective Sensors](https://www.mouser.com/ProductDetail/512-QRE1113f) qty(48)
- [6 pin female headers](https://www.mouser.com/ProductDetail/437-8018700610001101) 7mm high, 0.1" spacing, qty(~36)
- [22ohm resistors](https://www.mouser.com/ProductDetail/Xicon/266-22-RC?qs=sGAEpiMZZMvrmc6UYKmaNXFefT4dxyTCwtpTxTI0yoo%3D), bussed, qty(3)
SIP Packaged, bussed
- [100k ohm resistors](https://www.mouser.com/ProductDetail/IRC-TT-Electronics/L091S104LF?qs=sGAEpiMZZMvrmc6UYKmaNdnTrsZX%2FuSiyGduauH5Qpc%3D) bussed, qty(6)
SIP-9, 8 resistors, 9 pins
- Shift resgisters, qty(6)
[74HC165](https://www.mouser.com/ProductDetail/Texas-Instruments/CD74HC165EE4?qs=%2Fha2pyFadui%2FKTy9HJ5lB%2FBJ0Xswdr%252BnXu7asThazxrcGD%2FXuYTSNA%3D%3D)
- [3.3V Regulator](https://www.mouser.com/ProductDetail/Microchip-Technology/MCP1826S-3302E-AB?qs=sGAEpiMZZMsGz1a6aV8DcJ7KfjtCj7Xd5CqQpyOghgk%3D), (input, ground, output - IGO, pinout), qty(1)
- [screw terminals](https://www.mouser.com/ProductDetail/490-TB006-508-02BE) Two pin, 0.1", qty(3-4)
- [0.1 uF Ceramic Capacitor](https://www.mouser.com/ProductDetail/594-K104K15X7RF53H5), through hole
- [1 uF Ceramic Capacitor](https://www.mouser.com/ProductDetail/594-K105Z20Y5VF5TL2), through hole
- [560uF, 6.3V Capacitor](https://www.mouser.com/ProductDetail/661-APSC6R3L561MH08S)
low esr, 3.5mm lead spacing, 8mm diameter
- N-Channel Mosfet [FQP30N06](https://www.mouser.com/ProductDetail/512-FQP30N06L), qty(2)

#### Alternative pricing
Someone pointed out some alternative pricing that can really bring the parts cost
- [QRE1113 Reflectance Sensors](https://lcsc.com/product-detail/Photo-Interrupter_Everlight-Elec-ITR8307_C63451.html) ~$0.13/each @ qty(48)
- [6 pin female headers](https://lcsc.com/product-detail/Pin-Header-Female-Header_BOOMELE-Boom-Precision-Elec-C40877_C40877.html) 8.5mm high. ~$0.05/each @ qty(36+)
- [22 ohm SIP](https://lcsc.com/product-detail/Resistor-Networks-Arrays_FH-Guangdong-Fenghua-Advanced-Tech-A09-220JP_C9105.html) 8 resistor, 9 pin, it will fit. $0.44 for qty(6)
- [100k SIP Resistors](https://lcsc.com/product-detail/Resistor-Networks-Arrays_FH-Guangdong-Fenghua-Advanced-Tech-A09-104JP_C9108.html) 8 resistor, 9pin, it will fit. $0.44 for qty(6)

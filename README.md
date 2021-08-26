# Printed Circuit Boards for Duino Coin

This project is designed for making a solid and stable platform for Mining DUCO. The main idea is to build by yourself a cheap ASIC device, based on market prices and alternative components to reduce drastically the ROI time.
Beyond the stetic, size, power consumption, if this PCB is cheapper to build than buy many arduinos, then this project is viable.

In summary all designs consist in two separate groups:
1. Slaves microcontrollers: It's purpose is to do mining.
2. Master: It's purpose is to manage the connection between the server and slaves microcontrollers.

**If you're planning build this PCB, I invite you to read the whole article**

## Main Features

1. Microcontrollers supported: ATmega328P-AU , ATmega168-20AU , ATmega168PA-AU , ATmega8-16AU
1. PCBs less than 10x10cm (specially for low cost production)
2. 0603 components (more reliable, small, power friendly)
3. Compact size, you can store anywhere
4. No heat, you don't need heatsinks or fans (no noise)
5. Don't need a PC or a huge host to connect your rig to the server (that's the "master" duty)


## How to Order PCB's

If you think that the board is enough and you dont need to modify it, then download the `gerber.zip` file and that's all. PCB manufacturer will ask for that file in order for you to start building the board.
There are a lot of chinese webpages where you can order 5 units for about 2-10 dollars, just choose one where the shipping cost isn't too high in your country. For low cost worldwide shipping via EMS, e-packet, national post, usually cost arround 5-8 dollars shipping, (DHL or Fedex are the most expensive)

Some popular sites:

[All PCB](https://www.allpcb.com/?Mb_InviteId=69183) (Recomended, high quality and cheap PCBs)

[PCBway](https://www.pcbway.com/setinvite.aspx?inviteid=432106)

## How to Order Components

Here is a clasificate information. The main problem to order small amounts of components are the high shipping cost. The most convenient way to order components is if you have a friend that orders on popular and trusted sites like [Mouser](https://www.mouser.com/) then ask him to include your parts in the batch (then you can save a lot on shipping cost, actually free). Obviusly if you pay exactly for your parts, your friend will earn on the tax return on custom, so everybody wins.

But like all mortals in the world, the second best option is to order via Aliexpress. **I Include a file with some aliexpress link**, so you can quote and order them separately. Actually they are cheap if you buy low-medium amounts.

Don't forget also quote on your local electronic stores because maybe maybe is convenient buy them locally than order them.

## How to Build your Board

I can't teach you how to solder SMD (Surface Mount Device) components, but i could suggest some tutorials and tips that may help you a lot

First you need some basic tools. **Without them is impossible to build it**

1. Soldering Iron and thin tip (suggested tip 900M-T 1C or 900M-T 2C those are my favorite)
2. Soldering Wire, best quality you can get, 0.5mm recomended or lower for SMD components, 0.8mm - 1.0mm for the rest of components
3. Isopropilic Alcohol (to clean your board once finished)
4. Flux Paste, best quality you can get (liquid flux is terrible, avoid use liquid flux)
5. A pair of thin tweezers (ESD-15 my favorite)

There are some other tools that can help you a lot in the step of soldering. **The following tools are optional**


1. Soldering Station with hot air gun (suggested temperature 290°C at the most lower air flow)
2. Soldering paste, best quality you can get (do not try to melt soldering paste with the soldering iron, it will be a mess, use only with hot air)
3. Stencil: is an aluminium template that allow to apply soldering paste on every pad without doing much effort. Its a little expensive, so if you're planning to make many boards (5 boards or more, i suggest order stencil too).

**Use hot air and soldering paste are the best results, almost like a factory finishing** depends on your skills.

4. Digital Multimeter, will help you to check continuty and see if everything is ok.
5. Digital Microscope (?) 0603 components are bigger, this is really optional but if you're 20-50 years old probably you will not need it.


**Building**
Just some tips before start soldering

1. Print the schematics or have it in hand. All components are labeled on the PCB so you want to place the correct component on the correct pad.
2. Clean your board before soldering
3. Check the polarity of the components.
    Tantalium capacitor: the mark indicates the cathode (positive +)
    Electrolitic capacitor: The black paint mark indicates the anode (ground -)
    Ceramic capacitor: no polarity
    Resonator (or crystal): no polarity
    Microcontrollers: it has a point mark on the top left, it has to match on the PCB footprint
    Leds: The green mark on the bottom indicates the anode (ground -)
4. THT (through hole components) solder them at the end, pin headers, terminals, etc.
5. Once finished soldering, double check the conection, measure continity of the components.

I leave some tutorials: (Soldering iron)

[Tutorial English](https://www.youtube.com/watch?v=f9fbqks3BS8)
[Tutorial Spanish](https://www.youtube.com/watch?v=yil-EmlQMkg)

Tutorial with hot air gun

[Turorial English](https://www.youtube.com/watch?v=2Z7nCAxS2Rg)
[Tutorial Spanish](https://www.youtube.com/watch?v=qP4GwNsn8VI)

Once your board is finished, next step is to program your board


## How to program AVR ATmega Based Microcontroller

When you buy an ATmega microcontroller directly from the factory, it comes clean, without any code and bootloader pre-loaded. There are two steps here before mining.

**1. Burn the bootloader**

To do it you need an SPI to USB interpreter. There are manys. like "USBtinnyISP", "USBasp" or any arduino board (arduino uno, arduino nano, arduino mega, arduino leonardo, etc...)

On the case you use an arduino board, you need to load the example code.

file > examples > 11.  ArduinoISP (and you load that code).

Once you're done, you have to make the wiring
| Adapter | > | Your Board |
| ------------- | -- | ------------- |
| SCK | > | SCK |
| MISO | > | MISO |
| MOSI | > | MOSI |
| RESET | > | RESET |

In case you use an arduino you need to make this wiring
| Aduino | > | Your Board |
| ------------- | -- | ------------- |
| pin 13 | > | SCK |
| pin 12 | > | MISO |
| pin 11 | > | MOSI |
| pin 10 | > | RESET |

Also connect
| | | |
| ------------- | -- | ------------- |
| VCC | > | 5v |
| gnd | > | GND |

Once its wiring and connected, plug your adapter or arduino to USB and you should hear a device detected on USB port as COM3, COM4, COM5, etc... (you can check it on device manager)

On arduino IDE, go to tools and select the board (depends on the chip, but most of 99% of atmega328p -AU, the chip i design this board) uses AVR Arduino Boards > Arduino Nano
Go to tools again an select Processor > "ATmega328P (old bootloader)"
Go to tools again and select the port (where is connected your USB device, COM3? COM4?)

finally Go to tools again and select your Programmer (wich device are you using as SPI, USBtinnyISP", "USBasp" or "Arduino as SPI")

Then go to tools one more time and hit the last option "Burn bootloader"
If everything is ok, the led_build should blink twice every 1 second
Do it with every ATmega, so dont change anything... just unplug the USB, unplug the JST connector, move to the next chip plug the JST connector, plug your USB, once it detects the COM, hit "burn bootloader"

Possible trouble shootings:
Sometimes the first load fails (thats normal), hit again "burn bootloader" and it should burn fine (at the second time)
This occours because it sends a pulse to reset the atmega328 and sometimes it does very fast. (capacitor missing).
In summary (first attempt fail, second attempt success) This is normal.

If for any reason the attempt to burn the bootloader keeps fails (third time, fourth time) that means that something wrong in the hardware.
1. check your wiring, that have solid contacts
2. check the order of wiring (maybe you switch something)
3. check the soldering quality, high chance there is a bad pin soldered on the pads, check with a multimiter the top of the atmega (without making preasure) with the pinout. Or check with a microscope.

**2. Upload Code**


2. the next step is to upload the code.
You need a TTL to USB converter.
Plug (your TTL > your board)
TX > RX
RX > TX
VCC > 5v
GND > GND
**DTR > (add 0.1uF between) RESET (if not, you need to reset manually, simulate a buttom with a jumper wiring)
(Board reset and GND ready to short)

First open your IDE and charge some necessary libraries:
https://github.com/ricaun/arduino-DuinoCoin
https://github.com/ricaun/ArduinoUniqueID
https://github.com/ricaun/StreamJoin
https://github.com/bblanchon/ArduinoJson
https://github.com/me-no-dev/ESPAsyncWebServer
https://github.com/me-no-dev/ESPAsyncTCP

Download as a zip
Then go to your arduino IDE, select "program" > add library > Add library.zip (and select one by one the libraries you downloaded)
Once it done, open your "DuinoCoin_Arduino_Slave" folder and open DuinoCoin_Arduino_Slave.ino file

You're ready, now plug your TTL USB device (with the board plugged obviusly)
It will detects as a diferent COM (most probably)
Go to tools and select the correct port.

Then hit the second icon under the "file" like an arrow facing to the right (upload buttom)
If you use DTR pin on the TTL all is automatically, it will pop a message "uploaded success

If you dont use DTR you need to reset manually, you need to press reset buttom (but there is no reset buttom)... you you need to short reset with GND with a jumper wire. Just a very short time, less than a second before it starts uploading the code.
When you hit upload, first it compiles, then it upload, before it starts upload you need to press reset.
What i do, is to hit upload, short reset and hold it, when it appears "uploading" then i release. And you're done. It tooks about 5 seconds.

Do the same for all atmegas, unplug USB, change JST connector to the next chip, plug USB, hit upload

Possible trouble shootings:

1. it doesnt upload or USB not detected: check TX RX connection.
2. step 1 checked but not working: see if atmega chip is properly soldered, check with a microscope or multimeter.
3. usb detected but still cant upload the code: check tools property, make use to select the correct board (arduino nano), the correct processor (ATmega328P (old bootloader)), the correct port (COMX).
4. it says "timeout" after compiling: you didnt press reset buttom (short reset with gnd) before it starts uploading





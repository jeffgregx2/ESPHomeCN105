# Mitsubishi CN105 ESPHome Hardware - PCB

The purpose of this project was to provide a production level microcontroller capable of running the ESPHome firmware controlling the Mitsubishi spit-mini heat pumps.  It was important that the hardware be robust and is expected to run for the life of the split-mini system.  A breadboard or other approach didn't work for me.

The other reason I created this project is I had never built any type of PCB-level hardware before.  Thus it was an opportunity to learn new skills (circuit design, KiCad, etc).  For those of you more skilled than I, all of the mistakes and design failures due to lack of knowledge that you find I would love to hear about - just be aware that I started totally clueless (and generally I still am).  

## Features
During the design of my module I wanted the following features:

 - Plug compatible with the cable provided by Mitsubishi when using the PAC-USWHS002-WF-2 wifi module.  It must be possible to simply unplug the PAC module and plug in this replacement module with no other changes.
 - Low heat generation - thus selection of 5v instead of 12v to avoid the added heat generation converting from 12v to 5v/3.3v.
 - Low power usage - since we don't know the actual power available on the 12v/5v power pins on the CN105 connector the goal is to keep the average/max power level as low as possible.
 - Modern hardware - leverage the most modern CPU hardware with low power usage.
 - Provide expansion capability via an exposed i2c port.
 - Ensure selected connectors are robust and lock in - avoid heat expansion/contraction disconnects.
 - Creation of a case that matches the case housing the PAC module.
 - Ensure that the entire project can be hand soldered.

It is definitely possible to create a smaller footprint project (likely 40% smaller), however it wasn't clear to me that it would gain anything especially since I wanted the module to be accessible after installation and thus within the access panel (of the units I own).  Since the PAC modules fit keeping that form factor would also fit.  Plus it would make soldering easier (not to be underestimated).

## Schematics
With this in mind I created the following schematic:

![PCB Schematic Diagram](/images/PCB-schematic.png)

Clearly this is a relatively simple design.  The most important elements are the inclusion of level shifters to convert from 5v <-> 3.3v ensuring that the CPU and CN105 voltages are appropriately accommodated.

## Layout

The next step is to design a 2-layer PCB that supports the above schematic.  Some care was taken to minimize the interference with the WiFi antenna.

![PCB Layout Diagram](/images/PCB-layout.png)

## Fabrication
Fabrication can be accomplished using whichever fabricator you wish.  Given the very small number of boards I wanted (5), I chose [PCBWay](https://www.pcbway.com/project/shareproject/Mitsubishi_ESPHome_CN105_Microcontroller_kicad_pcb_b5b72995.html).  This link will simplify creation of the V1.1 project board if you want to make one yourself. 

Alternatively, you can use whatever fabricator you want and build the board yourself using the following [Gerber files](/pcb_assembly/gerber).

### Parts lists
|Qty|Part Desc.|Link|
|--|--|--|
| 1 | CN105 Connector | [S05B-XASK-1](https://www.digikey.com/en/products/detail/jst-sales-america-inc/S05B-XASK-1/9951644) |
| 1 | I2C/Stemma | [S4B-PH-K-S](https://www.digikey.com/en/products/detail/jst-sales-america-inc/S4B-PH-K-S/926628) |
| 1 | Wavemaker ESP32-C6-Zero | [ESP32-C6-Zero-M](https://www.amazon.com/dp/B0D1K19W2Y?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1) |
| 1 | 1A 32V Fuse | [MFU0805FF01000P500](https://www.digikey.com/en/products/detail/vishay-beyschlag-draloric-bc-components/MFU0805FF01000P500/1202619) |
| 6 | RES 10K OHM 1% 1/8W | [CRGCQ0805F10K](https://www.digikey.com/en/products/detail/te-connectivity-passive-product/CRGCQ0805F10K/8576363) |
| 2 | MOSFET N-CH 50V 220MA | [BSS138](https://www.digikey.com/en/products/detail/onsemi/BSS138/244210) |

## Case
To complete the project I created a 3D printed case that is as close to the same dimensions as the original PAC wifi module.  It is a tooless design that simply snaps together (it does require a small screwdriver or really strong fingernails to disassemble).  

![PCB in Case](/images/Case-compare-front.png)

The case was printed using white PLA using quality settings (0.2mm, 15% infill, no supports, etc.).  While there is a bit of play in the PCB restraint system, I did aim for precision to have the top/bottom snap to fit, etc.    You can find the STL files for the top & bottom of the case in the [3d_case](/pcb_assembly/3d_case) directory.  If there is sufficient interest I can place them on printables.

## Final Notes

This project could be done with larger components, there is sufficient space.  However I wanted the opportunity to learn surface mount components and chose 805 size as a compromise.  It would also enable installation of some or all of the components at fabrication time if that was ever interesting to someone.


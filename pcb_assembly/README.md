# Mitsubishi CN105 ESPHome Hardware - PCB

The purpose of this project was to provide a production level microcontroller capable of running the ESPHome firmware controlling the Mitsubishi spit-mini heat pumps.  It was important that the hardware be robust and is expected to run for the life of the split-mini system.  A breadboard or other approach didn't work for me.

The other reason I created this project is I had never built any type of PCB-level hardware before.  Thus it was an opportunity to learn new skills (circuit design, KiCad, etc).  For those of you more skilled than I, all of the mistakes and design failures due to lack of knowledge that you find I would love to hear about - just be aware that I started totally clueless (and generally I still am).  

## Features
During the design of my module I wanted the following features:

 - Plug compatible with the cable provided by Mitsubishi when using the PAC-USWHS002-WF-1 & WF-2 wifi modules.  It must be possible to simply unplug the PAC module and plug in this replacement module with no other changes.
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

![PCB Schematic Diagram](/images/WF-1/PCB-V1.2-schematic.png)

Clearly this is a relatively simple design.  The most important elements are the inclusion of level shifters to convert from 5v <-> 3.3v ensuring that the CPU and CN105 voltages are appropriately accommodated.

## Layout

The next step is to design a 2-layer PCB that supports the above schematic.  Some care was taken to minimize the interference with the WiFi antenna.

![PCB Layout Diagram](/images/WF-1/PCB-V1.3-layout.png)

## Model Differences

Mitsubishi has released multiple PAC modules over the past few years compatible with the Mitsubishi Kumo Cloud smart control system for their ductless mini-split HVAC systems.   The last two released versions are as follows:

<html><table>
<tr><td>
<b>PAC-USWHS002-WF-1</b><br>
<img src="/images/WF-1/WF-1-Front.png" alt="Single connector view"><br>
Note that the WF-1 has a single connector - JST XA 2.5mm pin spacing
</td>
<td>
<b>PAC-USWHS002-WF-2</b><br>
<img src="/images/WF-2/WF-2-Front.png" alt="Dual connector view"><br>
The WF-2 has dual connectors - JST PA 2.0mm pin spacing
</td></tr>
</table>
</html>
It is important to note that the two modules do NOT use the same sized connector and thus the cables for them are not directly compatible (without an adapter).  If you wish to use this project confirm which version you need by looking at the module number on the PAC module and/or confirming with the connectors on the module.

## Moving Ahead
For instructions on how to build a version of this project compatible with your split-mini model click on the model number:
- [PAC-USWHS002-WF-1](/pcb_assembly/WF-1)
- [PAC-USWHS002-WF-2](/pcb_assembly/WF-2)

These instructions include links to PCBWay to simplify creating the PCB/obtaining fully assembled modules for a very modest price.  They also include all files necessary to use other fabricators.  For those of you comfortable with soldering size 805 SMT components this project is very approachable.  That said, you will likely need some level of magnification unless you have superior eyesight (I do not).

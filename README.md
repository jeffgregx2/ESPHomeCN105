
# Mitsubishi CN105 ESPHome Hardware Microcontroller

This project is inspired by the work done by [@echavet](https://github.com/echavet/MitsubishiCN105ESPHome) and [@GeoffDavis](https://github.com/geoffdavis/esphome-mitsubishiheatpump) (and others) reverse engineering the CN105 serial protocol for the Mitsubishi Split-Mini heat pumps.  Their work allows for complete control of those units via ESPHome instead of the Kumo Cloud offering from Mitsubishi.  One can argue that the ESPHome offering is superior including the ability to have complete control over important logic such as room temperature settings, etc.

## Quick Links

 - Setting up ESPHome/Home Assistant - [Configuration](/home_assistant/)
 - Pre-made Hardware - [ETSY]() (Coming Soon) 
 - Building the Hardware - DIY/PCBWay:  
    - [PAC-USWHS002-WF-1 Compatible module](https://www.pcbway.com/project/shareproject/Mitsubishi_ESPHome_CN105_Microcontroller_kicad_pcb_b5b72995.html)
    - [PAC-USWHS002-WF-2 Compatible module](https://www.pcbway.com/project/shareproject/Mitsubishi_ESPHome_CN105_Microcontroller_PAC_USWHS002_WF_2_plug_compatible_8670e686.html)

## Hardware
In order to use the ESPHome approach, appropriate hardware needs to be assembled and installed in (or next to) each split-mini to be controlled.  Most take DevKits and breadboards or otherwise construct controllers to be installed.  However I wanted something more production ready that was plug compatible with the Mitsubishi PAC-USWHS002-WF-1 and PAC-USWHS002-WF-2 wifi modules and had the exact same footprint allowing easy swapping between modules.

To this end I have designed a PCB board using an ESP32-C6 devkit and associated 3D printed case that is the same size of the module it is replacing as well as plug compatible.  If you already have the PAC-USWHS002-WF-1 or WF-2 module installed, you can simply unplug that module and plug this new module into its place.  In addition, this new module exposes an i2c port via a [STEMMA](https://learn.adafruit.com/introducing-adafruit-stemma-qt/what-is-stemma) compatible connector.   For more information on the PCB design, 3D case, etc. and how to create your own copy of the board please see [PCB_assembly](/pcb_assembly/).

## Software

In addition, I have included ESPHome include files that allow assembling thermostat devices for this device in Home Assistant far easier and repeatable - very helpful if you have multiple devices.  The result allows for YAML files that only contain substitutions and secret references.  The files and additional documentation is available [HERE](/home_assistant/).

![PCB Board described above](/images/WF-2/PCB_V1.3-with-case.png)
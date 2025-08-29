
# Mitsubishi CN105 ESPHome Hardware Microcontroller

This project is inspired by the work done by [@echavet](https://github.com/echavet/MitsubishiCN105ESPHome) and [@GeoffDavis](https://github.com/geoffdavis/esphome-mitsubishiheatpump) (and others) reverse engineering the CN105 serial protocol for the Mitsubishi Split-Mini heat pumps.  Their work allows for complete control of those units via ESPHome instead of the Kumo Cloud offering from Mitsubishi.  One can argue that the ESPHome offering is superior including the ability to have complete control over important logic such as room temperature settings, etc.

However, in order to use the ESPHome approach, appropriate hardware needs to be assembled and installed in (or next to) each split-mini to be controlled.  Most take DevKits and breadboard or otherwise construct controllers to be installed.  However I wanted something more production ready that was plug compatible with the Mitsubishi PAC-USWHS002-WF-2 wifi module and had the exact same footprint allowing easy swapping between modules.

To this end I have designed a PCB board using an ESP32-C6 devkit and associated 3D printed case that is the same size of the module it is replacing as well as plug compatible.  If you already have the PAC-USWHS002-WF-2 module installed, you can simply unplug that module and plug this new module into its place.  In addition, this new module exposes an i2c port via a [STEMMA](https://learn.adafruit.com/introducing-adafruit-stemma-qt/what-is-stemma) compatible connector.   For more information on the PCB design, 3D case, etc. and how to create your own copy of the board please see [PCB_assembly](/pcb_assembly/).

![PCB Board described above](/images/PCB_v1.1.png)

In addition, I have included ESPHome include files that allow assembling thermostat devices for this device in Home Assistant far easier and repeatable - very helpful if you have multiple devices.  The result allows for YAML files that only contain substitutions and secret references.  The files and additional documentation is available [HERE](/home_assistant/).

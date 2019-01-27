## Repetier FW for the Da Vinci 1.0 printer with an E3Dv6 extruder.

This is a fork of the excellent port of [luc-github/Repetier-Firmware-4-Davinci](https://github.com/luc-github/Repetier-Firmware-0.92).

This project adds the changes I have introduced to support the replacement of the stock extruder with an E3Dv6 extruder in my Da Vinci 1.0 first generation.

### HW Modifications ###

* Replaced the Da Vinci 1.0 stock extruder with an E3Dv6 extruder. 
Details of the modifications with 3D printed parts and pictures can be found in my [Da Vinci 1.0 E3Dv6 mod with Filament Sensor]( https://www.thingiverse.com/thing:3142498) page on thingiverse.
* Added wiring and soldered through-hole components to the mother board to connect the v6 30mm 12V extruder cooler fan and enable the FW to switch it on and off as was done for the original cooler fan.
* The filament sensor daughter board is reused and retaines its original functions of sensor and filament guide.
* The original 5V 40mm extruder cooler fan is reused as feature cooler fan using my [remixed 40mm fun duct](https://www.thingiverse.com/thing:3131742). For a quieter operation of the fan at low speeds connect a 470μF 25V electrolitic capacitor in parallel, making sure to respect the polarity of the leads.

### FW Modifications ###

* Added a new custom thermistor sensor table for the semitec 104GT-2 NTC thermistor that comes with the E3Dv6 kit.
Note that the table includes the R1=10kΩ and R2=4.7kΩ resistor network on the Da Vinci 1.0 mother board, so there is no need to remove the R1 resistor to reuse exsisting tables. To generate the table I have added the Dv10-E3Dv6-ThermistorTable.py python script that can be easily reused for other thermistors and resistor networks.
* Configured the FAN2 PDM pin to be used for the E3Dv6 30mm 12V extruder cooler fan.
* Configured the FAN PDM pin to be used for the 40mm 5V feature cooler fan.
* Changed the default extruder steps per mm to 104 from 99 after measurement (can be done in EEPROM).
* Enabled the overriding of version macro in Configuration.h to display your own 16 character message at boot time.
* Turned off the Z probe pin and bed auto leveling.
* Set the heated bed default manager to be PID (can be done in EEPROM).
* Changed the manual bed leveling points to 4 points only, one over each knobs and one over the center.
* Changed manual bed leveling display messages, removed point 5.
* Fix fan kickstart code to remove bug for which the kickstart never happened in any condition, by explicitly setting the fan max speed during kickstart interval.

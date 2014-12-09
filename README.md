Welcome to cheali-charger!
==========================

This project is an alternative firmware for a variety of lipo chargers,  
see [hardware](README.md#hardware)

Don't use it if You don't need to  
(not everything is implemented yet).  

Any feedback is very welcome!  
http://groups.google.com/group/cheali-charger

Features
--------
- Li-ion, LiPo, LiPo-4.30V, LiPo-4.35V, LiFe:
  - charging
  - fast charging
  - charging + balancing
  - discharging
  - balancing
  - storage
  - storage + balancing
- NiCd and NiMH:
  - charging, method: -dV/dT
  - discharging
  - cycling
- NiZn:
  - charging
  - fast charging
  - charging + balancing
  - discharging
  - balancing
- Pb: - not well tested!
  - charging
  - discharging
- Internal resistance display
  - single cell resistance
  - whole battery resistance
  - battery leads resistance
- Internal and external temperature monitoring
- Overcharge and overdischarge monitoring
- Input voltage monitoring
- Memory for 30 batteries
- LogView support
- CALIBATION!


WARNING
-------
Please [CALIBRATE](README.md#calibration) charger before use!  
Use an external temperature probe  
(if You like your house ;) )


Hardware
--------
**Atmega32 CPU:**
- G.T. POWER A6-10 200W
- IMAX B6 Charger/Discharger 1-6 Cells (clone, original)
- AC/DC Dual Power B6AC 80W RC Balance Charger/Discharger
- Turnigy A-6-10 200W Balance charger & discharger
- Turnigy Accucel-6 50W 5A Balancer/Charger w/ Accessories
- Turnigy Accucel-8 150W 7A Balancer/Charger
- Turnigy MEGA 400Wx2 Battery Charger/Discharger (800W)
- ... many more

**Nuvoton NuMicro M0517LBN CPU:**
- IMAX B6 Charger/Discharger 1-6 Cells


Usage:
------

After [flashing](docs/flashing.md) your charger the first thing you should do is  
to [calibrate](README.md#calibration) it, after that your charger is ready to use.

programming you charger:
- select a free battery slot (indicated as 1., 2.,...)
- go to "edit battery"
 - change battery type "Bat:"
 - set battery voltage (number of cells) "V:"
 - set battery capacity "Ch:"
 - set charge current "Ic:"
 - set discharge current "Id:"
 - set time limit "Tlim:" (can be unlimited)
 - press "create name"

charing/discharging...:
- select battery
- select program: "charge", "discharge"...
- you should see a "info" screen,  
  (if you hear some beeping, check your battery connections)
- hold the "start" button for 2s to start the program
- charger is working now, press "inc", "dec" to see more screens
- to exit the program press "stop"

Informations about [settings](docs/settings.md).

[Flashing](docs/flashing.md)
----------------------------

Calibration
-----------
Connect a NOT fully charged LiPo battery to the main leads
and the balance port.

go to: "options"->"calibrate":
- voltage calibration: go to "voltage"
   - use a voltmeter to measure the voltage of all cells and the power supply voltage (Vin)  
     and set voltage on Vin, Vb1, Vb2, .., Vb6  
     (only Vb1 is mandatory, battery main leads and balance port must be connected)
- charge current calibration: 
  - connect your ampere meter in series with the battery on the red wire! (+), use the 10A(20A) input  
  - disconnect the balance port
  - go to "I charge"  
    - go to: "50mA" (100mA on some versions)  
      press "start" button (current flow should be visible on ampere meter)  
      press "Inc", "Dec" buttons until the ampere meter shows 50mA (100mA on some versions)  
      press "start" button (to save)  
    - go to: "1000mA"  
      press "start" button  
      press "Inc", "Dec" buttons until the amperemeter shows 1000mA  
      press "start" button  
      WARNING: the battery will be charged with high current!
- discharge current calibration: go to "I discharge"  
    Repeat the same steps as before  
    WARNING: the battery will be discharged with high current!
- when needed: external (or internal) temperature probe calibration: go to "temp extern" ("temp intern")
    You have to set two calibration points

Done.

[Calibration - Expert (IMAX B6) - optional](docs/caligration_expert.md)
-----------------------------------------------------------------------

[Building from Source](docs/building.md)
----------------------------------------

Troubleshooting
---------------
**Atmega32 CPU:**
1. After flashing charger doesn't work (display shows squares):
  - download the *.hex again, use the "RAW" button in github
  - check the sha1 sum of the file, compare it with *.sha1:
    - linux: $sha1sum cheali-charger*.hex
    - windows: install [Microsoft File Checksum Integrity Verifier](http://www.microsoft.com/en-us/download/details.aspx?id=11533)
      - in cmd.exe: fciv.exe -sha1 -add cheali-charger-*.hex
2. The sha1 sum is correct and the charger still doesn't work (display shows squares):
  - reset atmega32 fuses using avrdude:
    - windows: avrdude.exe -patmega32 -cusbasp -Uhfuse:w:0xc5:m -Ulfuse:w:0x3f:m
    - linux:   avrdude     -patmega32 -cusbasp -Uhfuse:w:0xc5:m -Ulfuse:w:0x3f:m


Other useful materials
----------------------
TODO

Mailing list
------------

If you have any questions or suggestions please write to us at: cheali-chargerATgooglegroups.com  
or visit: http://groups.google.com/group/cheali-charger  
The mailing list is open for all.

Have fun!

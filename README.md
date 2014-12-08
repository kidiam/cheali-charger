Welcome to cheali-charger!

This project is an alternative firmware for a variety of lipo chargers.  
see: ![hardware](https://github.com/stawel/cheali-charger#hardware)

Don't use it if You don't need to  
(not everything is implemented yet).  

Any feedback is very welcome!  
http://groups.google.com/group/cheali-charger

Features
========
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
=======
Please CALIBRATE the charger before use!  
Use an external temperature probe.  
(if You like your house ;) )



Hardware
--------
Atmega32 CPU:
- G.T. POWER A6-10 200W
- IMAX B6 Charger/Discharger 1-6 Cells (clone, original)
- AC/DC Dual Power B6AC 80W RC Balance Charger/Discharger
- Turnigy A-6-10 200W Balance charger & discharger
- Turnigy Accucel-6 50W 5A Balancer/Charger w/ Accessories
- Turnigy Accucel-8 150W 7A Balancer/Charger
- Turnigy MEGA 400Wx2 Battery Charger/Discharger (800W)
- ... much more

Nuvoton NuMicro M0517LBN CPU:
- IMAX B6 Charger/Discharger 1-6 Cells


Usage:
======

To use the charger you need to ![calibrate](https://github.com/stawel/cheali-charger/blob/master/README.md#calibration-imax-b6-and-gt-power-a6-10-200w)  
it first.


Flashing
--------

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

Calibration - Expert (IMAX B6)
------------------------------
If you want to improve the accuracy of the balancing on the first two cells you can try  
to calibrate the voltage on the first three pins of the balance port.
BE AWARE THAT ON SOME CHARGERS THIS CAN BE DANGEROUS!!!

First check if you can safely proceed by using the following test:

- disconnect everything from the charger
- measure the resistance between GND and Pin "0" on the balance port  
  (this is the furthest pin from the battery terminals and is  
  common to all balance port connectors)
  you can use GND from ISP connector (programmer connector) or any other GND on the charger
- if the resistance is very low (less than 1k Ohm) STOP THIS PROCEDURE!

If the measured resistance is much higher than 1k Ohm you can proceed as follows:

- connect the power supply to the ImaxB6 and go to "options" -> "calibrate" -> "expert DANGER!"
  - connect a 1.5V battery and a resistor (1k Ohm to 10kOhm) in the following manner:  
    connect ImaxB6 GND to one end of the resistor, the other end to the negative pole of the battery,  
    and the positive pole of the battery to Pin "0" (as above) on the balance port  
    you can use GND from ISP connector (programmer connector)
  - with a multimeter measure the voltage between GND and Pin "0" on the balance port.
    Adjust "Vb0pin" to this value using the inc/dec buttons
  - disconnect the 1.5V battery
- repeat the same steps as before for Pin "1" (balance port first cell)  
  you can use a higer voltage battery ~4.20V
- repeat the same steps as before for Pin "2" (balance port seccond cell)  
  you can use a higer voltage battery ~8.40V
- you can repeat the same steps for the batteries (-) terminal  
  for that you should use a 1.5V battery


Troubleshooting
---------------
- After flashing charger doesn't work (display shows squares):
  - download the *.hex again, use the "RAW" button in github
  - check the sha1 sum of the file, compare it with *.sha1:
    - linux: $sha1sum cheali-charger*.hex
    - windows: install http://www.microsoft.com/en-us/download/details.aspx?id=11533
      - in cmd.exe: fciv.exe -sha1 -add cheali-charger-*.hex
- The sha1 sum is correct and the charger still doesn't work (display shows squares):
  - reset atmega32 fuses using avrdude:
    - windows: avrdude.exe -patmega32 -cusbasp -Uhfuse:w:0xc5:m -Ulfuse:w:0x3f:m
    - linux:   avrdude     -patmega32 -cusbasp -Uhfuse:w:0xc5:m -Ulfuse:w:0x3f:m


Mailing list
============
If you have any questions or suggestions please write to us at: cheali-chargerATgooglegroups.com  
or visit: http://groups.google.com/group/cheali-charger  
The mailing list is open for all.


Building from Source
====================
atmega32 - linux
----------------
dependencies: git, cmake, avrdude, avr-libc, gcc-avr
<pre>
user@~$ sudo apt-get install cmake avrdude avr-libc gcc-avr git
user@~$ git clone https://github.com/stawel/cheali-charger.git
user@~$ cd cheali-charger
user@~/cheali-charger$ ./bootstrap
user@~/cheali-charger$ make

flashing <charger> with USBasp:

user@~/cheali-charger$ cd src/hardware/atmega32/targets/<charger>
user@~/cheali-charger/src/hardware/atmega32/targets/<charger>$ ./progUSBasp.sh
</pre>

Now You should see a "cheali-charger welcome" screen.
Done.


nuvoton M0517 - linux
---------------------

dependencies: git, cmake, gcc-arm-none-eabi, openocd (patched)

<pre>
user@~$ sudo apt-get install git cmake  gcc-arm-none-eabi
user@~$ git clone https://github.com/stawel/cheali-charger.git
user@~$ cd cheali-charger
user@~/cheali-charger$ ./bootstrap-arm
user@~/cheali-charger$ make

flashing <charger> with st-link-V2 or stm32f4discovery:
(patched openocd needed)

user@~/cheali-charger$ cd src/hardware/nuvoton-M0517/targets/<charger>
user@~/cheali-charger/src/hardware/nuvoton-M0517/targets/<charger>$ ./progStLink.sh
</pre>

Now You should see a "cheali-charger welcome" screen.
Done.

atmega32 - windows
------------------
TODO

nuvoton M0517 - windows
-----------------------
TODO


Have fun!




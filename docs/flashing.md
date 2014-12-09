
Flashing
========

Flashing: atmega32 CPU charger
-------------------------------

- Connect a standard AVR ISP cable to the board:
  - G.T. POWER A6-10 200W:  
  ![isp](connectors/isp_GTPowerA6-10.jpeg)
  - IMAX B6 - original:  
  ![isp](connectors/isp_imaxB6.jpeg)
  - IMAX B6 - clone:  
  ![isp](connectors/isp_imaxB6_clone.jpeg)

- use any atmel flash tool you like (for example avrdude)
- set "Device" to: atmega32
- use the cheali-charger/hex/cheali-charger-GTPowerA6-10-0.33.hex file as "Flash"


Flashing: IMAX B6
-------------------------------

- Connect a AVR ISP to the board, make sure that you have the appropriate connector!
    - IMAX B6 - original: 
    - IMAX B6 - clone: https://github.com/stawel/cheali-charger/blob/master/docs/imaxB6/imaxB6-clone-front.jpg
- set "Device" to: atmega32
- use the cheali-charger/hex/cheali-charger-imaxB6-original-0.33.hex  (or cheali-charger-imaxB6-clone-0.33.hex) file as "Flash"


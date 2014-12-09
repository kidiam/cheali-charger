
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


atmega32 - windows
------------------
**Atmel Studio**
- install [Atmel Studio](http://www.atmel.com/tools/atmelstudio.aspx) and [cmake](http://www.cmake.org/)
- start a "Atmel Studio Command Prompt" and go to your cheali-charger directory.
- run:
<pre>
  s:\cheali-charger> cmake . -G "Unix Makefiles"
  s:\cheali-charger> make
</pre>
- hex file should be in s:\cheali-charger\src\atmega32\targets\[your charger]\cheali-charger*.hex


**cygwin**
- install [cygwin](https://www.cygwin.com/)
- in cygwin install: cmake avrdude avr-libc gcc-avr git make
- in cygwin run:
<pre>
  ~/cheali-charger$ ./bootstrap
  ~/cheali-charger$ make
</pre>
- hex file should be in ~/cheali-charger/src/atmega32/targets/[your charger]/cheali-charger*.hex


nuvoton M0517 - windows
-----------------------
- install [CooCox CoIDE](http://www.coocox.org/)
- import project: cheali-charger\CoIDE\cheali-charger.coproj
- build


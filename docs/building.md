
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
1. install [Atmel Studio](http://www.atmel.com/tools/atmelstudio.aspx) and [cmake](http://www.cmake.org/)
2. start a "Atmel Studio Command Prompt" and go to your cheali-charger directory.
3. run:
  s:\cheali-charger> cmake . -G "Unix Makefiles"
  s:\cheali-charger> make
4. hex file should be in s:\cheali-charger\src\atmega32\targets\[your charger]\cheali-charger*.hex

**cygwin**
1. install [cygwin](https://www.cygwin.com/)
2. in cygwin install: cmake avrdude avr-libc gcc-avr git make
3. in cygwin run:
  ~/cheali-charger$ ./bootstrap
  ~/cheali-charger$ make
4. hex file should be in ~/cheali-charger/src/atmega32/targets/[your charger]/cheali-charger*.hex


nuvoton M0517 - windows
-----------------------
1. install [CooCox CoIDE](http://www.coocox.org/)
2. import project: cheali-charger\CoIDE\cheali-charger.coproj
3. build


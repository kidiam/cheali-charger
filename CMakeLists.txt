cmake_minimum_required(VERSION 2.6)

SET(CMAKE_SYSTEM_NAME Generic)
SET(CMAKE_C_COMPILER avr-gcc)
SET(CMAKE_CXX_COMPILER avr-g++)

Project(cheali-charger-mod)

find_package(UnixCommands)

MACRO (TODAY RESULT)
    if(BASH)
        EXECUTE_PROCESS(COMMAND "date" "+%Y%m%d" OUTPUT_VARIABLE ${RESULT})
        string(REGEX REPLACE "(..)/(..)/..(..).*" "\\1\\2\\3" ${RESULT} ${${RESULT}})
        string(REGEX REPLACE "(\r?\n)+$" "" ${RESULT} ${${RESULT}})
    else(BASH)
        string(TIMESTAMP ${RESULT})
    endif(BASH)
ENDMACRO (TODAY)

TODAY(timestamp)
set(cheali-charger-project-name ${PROJECT_NAME})
set(cheali-charger-buildid ${timestamp})
set(cheali-charger-version 0.33m)
set(cheali-charger-eeprom-calibration-version 8)
set(cheali-charger-eeprom-programdata-version 51)
set(cheali-charger-eeprom-settings-version 56)

configure_file(src/core/Version.h.in src/core/Version.h)

message(STATUS "Compilation date: ${timestamp}")
message(STATUS "Project name: ${cheali-charger-project-name}")
message(STATUS "version: ${cheali-charger-version}")


if(ARM-Cortex-M0)
    message(STATUS "target: ARM-Cortex-M0")
    include(arm-compiler.cmake)
    add_subdirectory(src/core)
    add_subdirectory(src/hardware/imaxB6-clone-ARM-Cortex-M0)
else(ARM-Cortex-M0)
    message(STATUS "target: avr")

    include(avr-compiler.cmake)
    add_subdirectory(src/core/atmega32)

    add_subdirectory(src/hardware/50W-5A)
    add_subdirectory(src/hardware/50W-6A)
    add_subdirectory(src/hardware/200W)   
    add_subdirectory(src/hardware/200W-commondisplay)
    add_subdirectory(src/hardware/80W)
    add_subdirectory(src/hardware/400W)
    add_subdirectory(src/hardware/Turnigy-Accucel-8-150W-7A)
    
    add_subdirectory(src/hardware/50W-5A_zero_amp_idnus)
    add_subdirectory(src/hardware/50W-5A_strong_balancer_zero_amp_idnus)
    add_subdirectory(src/hardware/50W-5A_strong_balancer_idnus)

    add_subdirectory(src/hardware/50W-6A_zero_amp_idnus)
    add_subdirectory(src/hardware/50W-6A_strong_balancer_zero_amp_idnus)
    add_subdirectory(src/hardware/50W-6A_strong_balancer_idnus)

    add_subdirectory(src/hardware/200W_zero_amp_idnus)
    add_subdirectory(src/hardware/200W_strong_balancer_zero_amp_idnus)
    add_subdirectory(src/hardware/200W_strong_balancer_idnus)    

    add_subdirectory(src/hardware/200W-commondisplay_zero_amp_idnus)  
    add_subdirectory(src/hardware/200W-commondisplay_strong_balancer_zero_amp_idnus)  
    add_subdirectory(src/hardware/200W-commondisplay_strong_balancer_idnus)   

    add_subdirectory(src/hardware/80W_zero_amp_idnus)  
    add_subdirectory(src/hardware/80W_strong_balancer_zero_amp_idnus)  
    add_subdirectory(src/hardware/80W_strong_balancer_idnus)        

    add_subdirectory(src/hardware/400W_zero_amp_idnus)  
    add_subdirectory(src/hardware/400W_strong_balancer_zero_amp_idnus)    
    add_subdirectory(src/hardware/400W_strong_balancer_idnus)

    add_subdirectory(src/hardware/Turnigy-Accucel-8-150W-7A_zero_amp_idnus)  
    add_subdirectory(src/hardware/Turnigy-Accucel-8-150W-7A_strong_balancer_zero_amp_idnus)  
    add_subdirectory(src/hardware/Turnigy-Accucel-8-150W-7A_strong_balancer_idnus)      
endif(ARM-Cortex-M0)



# Displaylib
A test program + library to drive the Adafruit 1.54" eInk Display (Color Version) on the stm32f103 microcontroller.

## Pinout
This project uses the following pinout.
#### PA15..0:
###### Display pins
* PA0: ECS
* PA1: D/C
* PA2: (DEAD ON NUCLEO BOARD)SRCS
* PA3: SDCS

###### SPI
* PA4: SPI1_NSS
* PA5: SPI1_SCK
* PA6: SPI1_MISO
* PA7: SPI1_MOSI

###### Display pins
* PA8: RST

###### UART
* PA9: TX
* PA10: RX

###### Display pins
* PA11: BUSY
* PA12: new SRCS

* PA13...15: Reserved


## Building
I used a custom build system (see CMakeLists.txt) because I could not find any easier way at the time. This includes a custom reset_handler and some CMSIS files which are not included in this project.

Therefore, the best way to get this working is to just copy the source files into an existing project from the IDE of your liking.

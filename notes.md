# Notes
Contains some notes on the implementation and the used components.

## Display (Driver: il0373)
* update time of 180 seconds (27s full refresh time)
* 3.3/5V
* MSB first
* CPOL 0
* CPHA 0
* SPI MODE 0

DTM1 -> 0 -> Black
    -> 1 -> White

DTM2 -> 0 -> Red
    -> 1 -> None


#### Step by step init
| Init stage          | Command                   | Size | *    | *    | *    | *    | *    |
|:-------------------:|:-------------------------:|:----:|:----:|:----:|:----:|:----:|:----:|
| Set powersettings   | IL0373_POWER_SETTING      | 5    | 0x03 | 0x00 | 0x2b | 0x2b | 0x09 |
| Set boostersettings | IL0373_BOOSTER_SOFT_START | 3    | 0x17 | 0x17 | 0x17 |      |      |
| Power on            | IL0373_POWER_ON           | 0    |      |      |      |      |      |
| Wait for busy       |
| Set panel setting   | IL0373_PANEL_SETTING      | 1    | 0xCF |
| CDI config          | IL0373_CDI                | 1    | 0x37 |
| PLL config          | IL0373_PLL                | 1    | 0x29 |
| VCM config          | IL0373_VCM_DC_SETTING     | 1    | 0x0A |
| Wait for busy       |
| Set resolution      | IL0373_RESOLUTION         |
*Data


#### Adafruit init code
```c
const uint8_t il0373_default_init_code[] {
  IL0373_POWER_SETTING, 5, 0x03, 0x00, 0x2b, 0x2b, 0x09,
    IL0373_BOOSTER_SOFT_START, 3, 0x17, 0x17, 0x17,
    IL0373_POWER_ON, 0,
    0xFF, 200,
    IL0373_PANEL_SETTING, 1, 0xCF,
    IL0373_CDI, 1, 0x37,
    IL0373_PLL, 1, 0x29,
    IL0373_VCM_DC_SETTING, 1, 0x0A,
    0xFF, 20,
    0xFE};

```


## SRAM (IC: 23A640/23K640)
* 20 MHz theoretical speed
* MSB first
* CPOL 0
* CPHA 0
* SPI MODE 0

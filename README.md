
# rt-usb-9axis-imu3-stm32duino-fw

This software is a sample program for the [RT-USB-9axisIMU3](https://www.rt-shop.jp/index.php?main_page=product_info&products_id=4247) device.

The file RT-9DOF-IMU-V3-Quat.ino is forked from the [SparkFun_ICM-20948_ArduinoLibrary examples](https://github.com/sparkfun/SparkFun_ICM-20948_ArduinoLibrary/tree/main/examples).

## Flashing from the Arduino IDE

### Setting Up Dependencies
* Please refer to [SparkFun_ICM-20948_ArduinoLibrary](https://github.com/sparkfun/SparkFun_ICM-20948_ArduinoLibrary) and install the library.
  * Operation has been confirmed only with version 1.2.5.
#### Enable DMP functionality
* By default the DMP functionality is disabled in the library as the DMP firmware takes up 14301 Bytes of program memory.
* To use the DMP, you will need to:
  * Edit ICM_20948_C.h
  * Uncomment line 29: #define ICM_20948_USE_DMP
  * Save changes
  * If you are using Windows, you can find ICM_20948_C.h in:
  * Documents\Arduino\libraries\SparkFun_ICM-20948_ArduinoLibrary\src\util

### Setting Up STM32duino
Please add the following URL to "File" → "Preferences" → "Additional Boards Manager URLs":
https://github.com/stm32duino/BoardManagerFiles/raw/main/package_stmicroelectronics_index.json

Install "STM32 MCU based boards" from the Boards Manager.
Please also install the STM32CubeProgrammer tool, which is required to flash firmware to the STM32 microcontroller.

Please configure the board settings as follows:
- Board: Generic STM32G4 boards
- Port: DFU 1-4
- Board part number: Generic G431KBUx
- Upload method: STM32CubeProgrammer (DFU)
- USB support (if available): CDC (generic 'Serial' supersedes U(S)ART)

### Changing USB VID/PID
If necessary, you may change the relevant lines in boards.txt, which can be found in a directory such as:
C:\Users\<UserName>\AppData\Local\Arduino15\packages\STMicroelectronics\hardware\stm32\<version>

For the production version shipped by RT, the following VID and PID are used:
```
GenG4.vid.0=0x2b72
GenG4.pid.0=0x0014
```

### Flashing the Firmware
Start the device in BOOT mode (please power it on while holding the switch).
Power on the device in boot mode and proceed with flashing the firmware.

## Flashing the Binary
Please download the binary to be flashed from the [releases page](https://github.com/rt-net/rt-usb-9axis-imu3-stm32duino-fw/releases).
Please flash it using STM32CubeProg.


# rt-usb-9axis-imu3-stm32duino-fw

This software is a sample program for the [RT-USB-9axisIMU3](https://www.rt-shop.jp/index.php?main_page=product_info&products_id=4247) device.

The file RT-9DOF-IMU-V3-Quat.ino is forked from the [SparkFun_ICM-20948_ArduinoLibrary examples](https://github.com/sparkfun/SparkFun_ICM-20948_ArduinoLibrary/tree/main/examples).

## Data format
Baud rate: 2000000 bps  
Transmission frequency: 1 kHz

|Byte | Content | Description | 
|-- | -- | -- | 
|0 | 0xff | Header | 
|1 | 0xff | Header | 
|2 | 0x52 | ASCII code "R" | 
|3 | 0x54 | ASCII code "T" | 
|4 | 0x40 | Lower Bits of Product Identifier | 
|5 | 0x41 | Upper Bits of Product Identifier | 
|6 | 0x01 | FW version | 
|7 | 0x00~0xff | Timestamp - incremented with each data transmission, wraps to 0x00 after 0xff | 
|8 | ACC_X_L | ax=(ACC_X_L\|ACC_X_H<<8)/2048*9.8 [m/s] | 
|9 | ACC_X_H |  | 
|10 | ACC_Y_L |  | 
|11 | ACC_Y_H |  | 
|12 | ACC_Z_L |  | 
|13 | ACC_Z_H |  | 
|14 | GYRO_X_L | gx=(GYRO_X_L\|GYRO_X_H<<8)/(32767/2000)*PI/180 [rad/s] | 
|15 | GYRO_X_H |  | 
|16 | GYRO_Y_L |  | 
|17 | GYRO_Y_H |  | 
|18 | GYRO_Z_L |  | 
|19 | GYRO_Z_H |  | 
|20 | Q1_1 | Q1 multiplied by (2^30). q1=(Q1_1 \| Q1_2<<8 \| Q1_3<<16 \| Q1_4<<24 )/(2^30) | 
|21 | Q1_2 |  | 
|22 | Q1_3 |  | 
|23 | Q1_4 |  | 
|24 | Q2_1 |  | 
|25 | Q2_2 |  | 
|26 | Q2_3 |  | 
|27 | Q2_4 |  | 
|28 | Q3_1 |  | 
|29 | Q3_2 |  | 
|30 | Q3_3 |  | 
|31 | Q3_4 |  | 
|32 | Checksum | Lower 8 bits of the sum of all bytes | 


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

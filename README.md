# stm32flash

Modified version to support GigaDevice MCU. Original: http://stm32flash.sourceforge.net/

add option '-G' to switch between STM32 and GD32 MCU

##Usage:

### Get GigaDevice Info.
stm32flash contains two arrays that map the device id to compiled-in information about SRAM/Flash/Bbootloader/Option Bytes.
The newly added commandline option switches between device tables for STM32 and GD32 devices.

New GD32 MCU must be added to the gd32_devices[].<br>
GD32E103TBxx uses same device ID as STM32, but SRAM size, Flash size and page size differ. Using stm32 information to flash GigaDevice will erase invalid pages


~~~sh
 ./stm32flash -G -b 115200 -S 0x8010000 -w t.txt /dev/ttyUSB0
stm32flash 0.7

http://stm32flash.sourceforge.net/

Using Parser : Raw BINARY
Location     : 0x8010000
Size         : 6
Interface serial_posix: 115200 8E1
Version      : 0x22
Option 1     : 0x00
Option 2     : 0x00
Device ID    : 0x0418 (GD32E103TBxx)
- RAM        : Up to 32KiB  (0b reserved by bootloader)
- Flash      : Up to 128KiB (size first sector: 1x1024)
- Option RAM : 16b
- System RAM : 18KiB
Write to memory
Erasing memory
Wrote address 0x08010006 (100.00%) Done.
~~~

### Flashing example
~~~sh
  # flash full file
  stm32flash -G -b 115200 -w ~/Downloads/rfid118-HW-V1.0-D0770-V0.1.bin /dev/ttyUSB0

  # flash only first n bytes to specific start address
  stm32flash -G -b 115200 -w ~/Downloads/rfid118-HW-V1.0-D0770-V0.1.bin -S 0x8010000:10000 /dev/ttyUSB0
~~~

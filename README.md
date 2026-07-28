# STM32C5-eval-board

Custom STM32C5 board in the breadboard friendly BluePill format designed in Kicad v10.

**Features**

- Compact breadboard friendly board size at 53.5mm x 20mm with 2x16 pin headers.
- STM32C551CE Cortex-M33 MCU, 144 MHz, 512 KB flash, 128 KB RAM. ([Product page](https://www.st.com/en/microcontrollers-microprocessors/stm32c551ce.html) / [Datasheet](https://www.st.com/resource/en/datasheet/stm32c551ce.pdf))
- USB-C power connection with CH340E uart to usb bridge (USART1 used).
- LSE 32768 Hz crystal and HSE with 24 MHz crystal.
- 3V3 LDO with power status led (red).
- Reset button.
- User led (green) and user button.
- SWD header for programming (Must be used as BOOT0 is not exposed).
- All other MCU pins is routed to board edge headers.

**Note** 

This MCU familiy is quite new and therefore not all variants of this MCU was available with the usual suppliers
when this board was created. When other variants with LQFP-48 footprints is available this should be pin compatible
with the layout of this board.

**Pinout** 

<img width="1240" height="1754" alt="stm32c5-evaluation-board-pinout" src="https://github.com/user-attachments/assets/df42aa17-1694-4b66-a82b-5cc468259c86" />

For pin alternative function definitions it is recommended to use the STMicroelectronics application CubeMX2.

**Production**

Production files adapted to [PCBWay](https://www.pcbway.com/) recommendations is found in the *fab* folder.

**Firmware**

As this is a new MCU familiy I could only get the STMicroelectronics original software
and hardware to work with flashing the device. SEGGER's J-Link Debug Probe will also
probably support this MCU familiy.

In the *firmware* folder there is a project file for CubeMX2. By opening this file
it as matter of generate the CMake project files.

I used VSCode and the CubeMX extension to open the generated CMake project files and
added the following test code for a simple blinker application:

```C++
/*
  * You can start your application code here
  */

while (1) {
  printf("hello!\n");
  HAL_GPIO_TogglePin(HAL_GPIOB, HAL_GPIO_PIN_9);
  HAL_Delay(2000);
}
```

**Testing**

[board-testing.webm](https://github.com/user-attachments/assets/a6211ade-eac5-4887-8b39-223c8f42b538)

The board has been verified to work correctly with the uart-to-usb bridge, leds, buttons
and crystals. The only minor issue was that the SWDIO and clock pin was swapped.

This will be fixed in a future revision along with any other issue.

**TODO** 

- Fix SWD CLK/DIO swap on silkscreen and schematic.
- Possible expose BOOT0 with a test point on PCB.
- Possible add PCB jumper to disconnect power led for battery operations.

**Sponsors** 

This board was generously sponsored by [PCBWay](https://www.pcbway.com/) and this project was handled
in quick and professional way in my experience. Thanks.

**Acknowledgments**

This board was developed and with help of and inspiration by the excellent instruction videos on the [Phil's Lab](https://www.youtube.com/@PhilsLab)
Youtube channel.

Also initially skeptical to KiCAD software, it turned out to be a very nice experience working with this application.
The team behind KiCAD does an excellent job in turning this application into a professional tool.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

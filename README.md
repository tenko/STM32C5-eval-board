# STM32C5-eval-board

Custom STM32C5 board in the breadboard friendly BluePill format designed in Kicad v10.

**Features**

- Compact 53.5mm x 20mm board size with 2x16 pin headers.
- STM32C551CE Cortex-M33 MCU, 144 MHz, 512 KB flash, 128 KB RAM. ([Product page](https://www.st.com/en/microcontrollers-microprocessors/stm32c551ce.html) / [Datasheet](https://www.st.com/resource/en/datasheet/stm32c551ce.pdf))
- USB-C power connection with CH340E uart to usb bridge (USART1 used).
- LSE 32768 Hz crystal and HSE with 24 MHz crystal.
- 3V3 LDO with power status led (red).
- Reset button.
- User led (green) and user button.
- SWD header for programming (Must be used as BOOT0 not exposed).
- All other MCU pins routed to board edge headers.

**Note** 

This MCU familiy is quite new and therefore not all variants of this MCU was available with the usual suppliers
when this board was created. When other variants with LQFP-48 footprints is available this should be pin compatible
with this board.

**Flashing Firmware**

As this is a new MCU familiy I could only get the STMicroelectronics original software
to work with flashing the device. Also the original flash tools from STMicroelectronics
is needed here.

**Testing**

<video src="board-testing.webm" autoplay loop muted playsinline width="100%"></video>

The board has been verified to work correctly with the uart-to-usb bride, leds, buttons
and crystals working correctly. The only minor issue was that the SWDIO and clock pin
was swapped. This will be fixed in a future revision along with any other issue.

**Sponsors** 

This board was generously sponsored by [PCBWay](https://www.pcbway.com/) and this project was handled
in quick and professional way in my experience. Thanks.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

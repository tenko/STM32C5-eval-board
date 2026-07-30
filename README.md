# STM32C5-eval-board

Custom *STM32C5* board in the breadboard friendly *BluePill* format designed in *Kicad v10*.

**Features**

- Compact breadboard friendly board size at 53.5mm x 20mm with 2x16 pin headers.
- STM32C551CE Cortex-M33 MCU, 144 MHz, 512 KB flash, 128 KB RAM. ([Product page](https://www.st.com/en/microcontrollers-microprocessors/stm32c551ce.html) / [Datasheet](https://www.st.com/resource/en/datasheet/stm32c551ce.pdf))
- USB-C power connection with CH340E uart to usb bridge (USART1 used).
- LSE 32768 Hz crystal and HSE with 24 MHz crystal.
- 3V3 LDO with power status led.
- Reset button.
- User led and user button.
- SWD header for programming (Must be used as BOOT0 is not exposed).
- All other MCU pins is routed to board edge headers.

**Note** 

This MCU family is quite new and therefore not all variants of this MCU was available with the usual suppliers
when this board was created. When other variants with *LQFP-48* footprints is available this should be pin compatible
with the layout of this board.

**Pinout** 
<img width="1240" height="1754" alt="stm32c5-evaluation-board-pinout" src="https://github.com/user-attachments/assets/db8b2e88-2932-41d7-97e5-1e8a8a481122" />

For complete pin alternative function definitions it is recommended to use the *STMicroelectronics* application *CubeMX2*.

**Production**

Production files adapted to [PCBWay](https://www.pcbway.com/) recommendations is found in the *fab* folder.

**Firmware**

As this is a new MCU family I could only get the *STMicroelectronics* original software
and hardware to work with flashing the device. *SEGGER's J-Link* Debug Probe will also
probably support this MCU family.

In the *firmware* folder there is a project file for *CubeMX2*. By opening this file
it as matter of generate the *CMake* project files.

I used *VSCode* and the *CubeMX* extension to open the generated *CMake* project files and
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

**Alternative Firmware in Oberon-2**

As an alternative to *C/C++* the [ECSOberon](https://ecs.openbrace.org/) language and the
[ECSMicroLib](https://github.com/tenko/ECSMicroLib/) framework can be used to develop
firmware for this board.

**ECSOberon** has a number of benefits for MCU applications:

- Simplest possible language (the [language report](https://github.com/OberonSystem3/TheOberonCompanionCD/blob/main/Papers/Oberon2.pdf?raw=true) is 20 pages), yet supporting 
  object oriented design with single inheritance.
- The language has the bit SET type which makes fiddling with bit register of the MCU very easy and natural.
- The ECSOberon language is updated with manual allocation, unsigned types, variable pointers, packages and simple templates.
  Making the language more practical for system programming and MCUs than the original Oberon-2 implementation.
- No header files to worry about. The visibility of the code elements is defined directly in the module.
- The module and package concept keeps the code cleanly segregated and avoid the problem with colliding names in C.
- The [documentation](https://ecs.openbrace.org/manual/) is excellent and reported bugs is fixed quickly.

The drawback of **ECSOberon**:

- *Oberon-2* is a verbose language and require upper case keyword.
  However with an IDE and auto-completion this is a minor issue in my opinion.
- No support for a pre-processor. Some cases can be solved with help of templates, but otherwise
  this must be solved with shell scripts.
  However this omission keeps the code base readable in my opinion.
- Not much existing code exists and many things must be implemented from scratch.
  I have a project [ECSStdLib](https://github.com/tenko/ECSStdLib/) covering some basic areas for me.
  Also much code from the original [OberonSystem 3](https://github.com/OberonSystem3) can be reused.
  This is the major drawback in my opinion.

**Testing**

[board-testing.webm](https://github.com/user-attachments/assets/a6211ade-eac5-4887-8b39-223c8f42b538)

The board has been verified to work correctly with the uart-to-usb bridge, leds, buttons and crystals.

Minor issues:

- The *SWDIO* and *SWDCLK* pin was swapped.
- The silkscreen was difficult to read.

This will be fixed in a future revision along with any other issue.

**TODO** 

- Fix *SWD CLK/DIO* swap on silkscreen and schematic.
- Possible expose *BOOT0* with a test point on PCB.
- Possible add PCB jumper to disconnect power led for battery operations.
- Review pins used for user button/led and usb-to-uart.

**Sponsors** 

This board was generously sponsored by [PCBWay](https://www.pcbway.com/) and this project was handled
in quick and professional way in my experience. Thanks.

**Acknowledgments**

This board was developed and with help of and inspiration by the excellent instruction videos on the [Phil's Lab](https://www.youtube.com/@PhilsLab)
Youtube channel.

Also initially skeptical to *KiCAD* software, it turned out to be a very nice experience working with this application.
The team behind *KiCAD* does an excellent job in turning this application into a professional tool.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

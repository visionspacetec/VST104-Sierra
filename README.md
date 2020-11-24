# VST104 Board Sierra - single MCU OBC for PC104 CubeSats
This repository contains the KiCad project and other documents created during the development of Board Sierra under [VST104 project](https://github.com/visionspacetec/VST104/). This PC104 CubeSats module is a single redundant onboard computer designed to fulfill most space industry requirements.

<p align="center">
  <br>
  <img src=/gallery/3Dexport/top.png width=49%/>
  <img src=/gallery/3Dexport/bottom.png width=49%/>
  <br><br>
  <b>Fig 1.</b> Board Sierra OBC module 3D visualisation top (left) and bottom (right) side.
  <br><br>
</p>


## Basic specifications
* **`processor:`** This onboard computer is driven by state of the art, ultra-low-power STM32L496 ARM® Cortex®-M4 core microcontroller. This MCU is capable of running up to 78[MHz] in our design.
* **`clock:`** Microcontroller is driven by two external clock sources. Low-speed external 32.768[kHz] oscillator (LSE) and high-speed external 26[MHz] oscillator (HSE). The MCU is capable of temporarily disable the HSE to achieve better power consumption.
* **`memory:`** Two groups of triple redundant external memories are available for data storage and processing. The triple redundancy was chosen as an effective measure against single event effects. The first memory group is 256 [Mbit] Flash wired via Quad-SPI interface and the second one is 2 [Mbit] F-RAM using SPI.
* **`peripherals:`** This module can communicate with other CubeSat subsystems using a wide variety of redundant protocols. The main PC104 header is capable of connecting to 2x CAN-BUS, 3x I2C, 4x UART (with CTS and RTS), 2xSPI (2 enables each), and 22 general purpose A/D I/O pins. All of the listed peripherals are wired thru separated isolators controlled by the MCU. On top of that, separate traces are used for system check and maintenance signals, such as: WatchDog, KillSwitch, CPUmode, Sync, FaultCollector. The pinout of these interferences is shown in figure 3.
* **`connectivity:`** A user can program and debug this OBC using SWI and/or UART interface. These interfaces are accessible on the board's edge on a separate connector with integrated electrostatic discharge protection circuitry. The SWI interface is compatible with STM ST-LINK series programmers (including SWO pin).

<p align="center">
  <br>
  <img src=/gallery/present/modules.png width=100%/>
  <br><br>
  <b>Fig 2.</b> Important circuitry groups on top (left) and bottom (right) side of the module.
  <br><br>
</p>

## Features
* All used components are suitable for the space environment, following: mechanical failure qualifications AEC-Q100 or AEC-Q200 and military rated operational temperatures (-40°C to +125°C).
* This module requires two separate power lines of 3.3[V] and 5[V] ratings. A robust power management circuitry is present separately on these lines, providing various functionalities. Namely: tunable over and under-voltage protection, tunable over-current protection, amplified current monitoring output, kill switching, or simultaneous power down.
* A group of seven I2C temperature sensors is spread over the entire module. These sensors are used to check the temperature of essential submodules such as: 2x power management, 2x CAN-BUS drivers, 2x external memories, and 1x STM32 microcontroller. Also, the MCU can power these sensors in case of power saving or latch-up events.
* A compact design was one of our priorities during the development of this module. As a result, this module's full three-fourths are left empty and ready to accommodate any required payload. This current version is the payload sector represented as a universal soldering array with exposed power lines (outside the power management).

<p align="center">
  <br>
  <img src=/gallery/present/header_pinout.png width=50%/>
  <br><br>
  <b>Fig 3.</b> PC104 header pinout supported by this OBC module.
  <br><br>
</p>

## Debug & Program connector
A separate 2x4 female format connector on the board's left side is used for debugging and programming.  SWI and UART5 interfaces of the boarded STM32 microprocessor are wired to this connector, as shown in figure 4. This interface is fully compatible with STM ST-Link family programmers. 

<p align="center">
  <br>
  <img src=/documents/deb_prog_pinout.png width=50%/>
  <br><br>
  <b>Fig 4.</b> Pinout of the debug and program connector.
  <br><br>
</p>

## References
The design of this PC 104 SBC module was processed under evaluation of the following documents:

[1] : [STM32L496xx datasheet](https://www.st.com/resource/en/datasheet/stm32l496ae.pdf)  
[2] : [STM32L496xx getting started manual](https://www.st.com/resource/en/application_note/dm00125306-getting-started-with-stm32l4-series-and-stm32l4-series-hardware-development-stmicroelectronics.pdf)  
[3] : [STM32 oscillator design guide](https://www.st.com/resource/en/application_note/cd00221665-oscillator-design-guide-for-stm8afals-stm32-mcus-and-mpus-stmicroelectronics.pdf)  
[4] : [STM32 Quad-SPI interface](https://www.st.com/resource/en/application_note/dm00227538-quadspi-interface-on-stm32-microcontrollers-and-microprocessors-stmicroelectronics.pdf)  
[5] : [Common mode chokes in CAN networks](https://www.ti.com/lit/an/slla271/slla271.pdf?ts=1593763769749&ref_url=https%253A%252F%252Fwww.google.com%252F#:~:text=In%20general%2C%20common%2Dmode%20chokes,results%20in%20the%20CAN%20network.&text=Following%20the%20choke%20in%20the,is%20the%20optional%20termination%20circuit.)  
[6] : [Isolated CAN systems with protection](https://www.ti.com/lit/an/slla419/slla419.pdf?ts=1593773861416&ref_url=https%253A%252F%252Fwww.google.com%252F#:~:text=A%20bidirectional%20TVS%20diode%20can,ratings%20up%20to%20several%20kilowatts.)


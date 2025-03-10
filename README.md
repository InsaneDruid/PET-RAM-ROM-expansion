# PET RAM & ROM - a 32K expansion for the PET 2001-8

While there are solutions to upgrade a PET 2001 to more than 4 or 8 Kb of RAM and use option ROMs in the 0x9000, 0xA000 and 0xB000 address range, these expansions usually sit in the processor socket and completely isolate the CPU from the PET motherboard during RAM and ROM access, turning the PET board into an I/O-only solution. While this is fine from a technical standpoint, I feel it destroys the spirit of retro computing and keeps the machines running, especially since all PETs have *some* designated expansion slot.

The PET RAM and ROM expansion utilizes the 2001's RAM/ROM expansion slot to expand - not replace - memory from 4 or 8 to a full 32 KB and to provide up to 2 switchable banks of expansion ROMs for the 0x9000, 0xA000 and 0xB000 address range. 

The physical design of the PET RAM & ROM is inspired by the Nestar Basic ToolKit extension.

![PET-RAM-&-ROM-EXPANSION render](https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/images/pet-ram-&-rom-expansion_render.png)

[Schematic](https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/pet-ram-&-rom-expansion.pdf "open Schematic")  

[Bill of Materials](https://htmlpreview.github.io/?https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/bom/pet-ram-&-rom-expansion_bom.html "open Bill of Materials")

## The RAM
A 62256 static RAM provides up to 28Kb of additional RAM, beginning at 0x1000 or 0x2000, selectable with the JP1 *4K* jumper:
* For PETs having 4K of on-board memory, bridge jumper *4K*
* For PETs with 8K memory, leave jumper *4K* open.

Note: The RAM expansion slot does not provide the SEL0 line, so at least 4k of PET onboard memory are required.

## The ROM
The ROM slot of the PET RAM & ROM can be populated with either RAM, battery backed RAM, EEPROMs or classic EPROMs giving the option of either fixed expansion ROMs or SOFTROM solutions.

### The EPROM option
The use of EPROMs is a cost-effective and simple method of equipping the PET with up to 2 banks of expansion ROMs in the 0x9000, 0xA000 and 0xB000 address range.

#### 27128 EPROM - provides one bank of 3 expansion ROMS.

* Prepare the ROM contents as follows:

| ROM address hex | ROM address dec | Content |
| :--- | ---: | ---: |
| 0x0000-0x0FFF | (0 - 4095) | unused |
| 0x1000-0x1FFF | (4096 - 8191) | 0x9000 expansion ROM |
| 0x2000-0x2FFF | (8192 - 12287) | 0xA000 expansion ROM |
| 0x3000-0x3FFF | (12288 - 16383) | 0xB000 expansion ROM |
	
#### 27256 EPROM - provides two banks of 3 expansion ROMS
* Install a switch between the pins of the ROM 14 header to switch between the 2 banks.
* Prepare the ROM contents as follows:

| ROM address hex | ROM address dec | Content |
| :--- | ---: | ---: |
| 0x0000-0x0FFF | (0 - 4095) | unused |
| 0x1000-0x1FFF | (4096 - 8191) | 0x9000 expansion ROM 1 |
| 0x2000-0x2FFF | (8192 - 12287) | 0xA000 expansion ROM 1 |
| 0x3000-0x3FFF | (12288 - 16383) | 0xB000 expansion ROM 1 |
| 0x4000-0x4FFF | (16384 - 20479) | unused                 |
| 0x5000-0x5FFF | (20480 - 24575) | 0x9000 expansion ROM 2 |
| 0x6000-0x6FFF | (24576 - 28671) | 0xA000 expansion ROM 2 |
| 0x7000-0x7FFF | (28672 - 32767) | 0xB000 expansion ROM 2 |

### The SOFTROM option
The use of SRAM or battery-backed, non-volatile SRAM with a size of 16kB or 32kB (e.g. 62256 SRAM or DS1230Y/AB non-volatile SRAM) offers a flexible solution that is ideal if the content of the expansion ROMs needs to change frequently.

16k x 8 RAM - provides one bank of 3 expansion SOFTROMS  
32k x 8 RAM - provides two banks of 3 expansion SOFTROMS.

* Install a switch between the pins of the *RAM WE* header to control the write enable line of the RAM.  
It is recommended to set this switch to open after loading the content into the SOFTROM.
* When using 32Kb RAM, install a switch between the pins of the *ROM 14* header to switch between the 2 banks.

Note: theoretical, EEPROMs can be used as well, though currently there is no viable EEprom programming software for BASIC2 available.

## The Firmware
The GAL16V8 (tested on ATF 16V8BQL15 PU) needs to be programmed with the [Firmware](https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/firmware "goto firmware folder"). A TL866/T48 eprom burner will do the job. Its *not neccessary to enable *encrypt chip* or to set the *lock bit*.

## The power source
Unfortunately, the 2001's RAM/ROM expansion slot doesn't provide any power pins, as RAM expansions thought to have their own power regulators and feed directly from the 2001's transformer.
The PET RAM & ROM though can be powered directly from the 5V available on the second tape port.

## The printable Backshell
To protect the backside of the board, and cover the power connector on the tape port, 3d printable parts are available.

![Back shell render](https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/images/pet-ram-&-rom-expansion_backshell_render.png)
[Printable back shell on printables.com](https://www.printables.com/model/1219181-cbm-pet-2001-expansion-cover/ "Printable back shell on printables.com") 

![Power connector housing render](https://github.com/InsaneDruid/pet-ram-rom-expansion/blob/main/images/power_connector_housing_render.png)
[Printable power connector housing on printables.com](https://www.printables.com/model/1219181-cbm-pet-2001-expansion-cover/ "Printable tape connector housing on printables.com")   


## The License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.  
See https://creativecommons.org/licenses/by-sa/4.0/.

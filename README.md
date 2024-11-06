# STM32H5 USB DFU Dual Bank demo
 
Two applications are included in the example.    
- Application_Example_for_STM32H5_USB_DFU_Dual_Bank: One is an example of an application code that simply blinks an LED and outputs some information on the terminal by UART.   
- STM32H5_USB_DFU_Dual_Bank: This is the USB DFU Bootloader that resides at the beginning of each bank to manage the firmware upgrade process and manage the dual bank of the STM32H5.

Please check the PDF document for more details.

## Hardware & Software needed

Hardware:
- [NUCLEO-H563](https://www.st.com/en/evaluation-tools/nucleo-h563zi.html) (using STM32H5 MCUs)
- 2x USB Cables

Software:
- [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html) (V1.15.0, do not use version V2.16.0 due to a limitation)
- Terminal Software like [TeraTerm](https://teratermproject.github.io/index-en.html)

## Materials Provided

- STM32H5 USB DFU Dual Bank Project (source and binary)
- STM32H5 Application Example Code (source and binary)
- STM32H5 USB DFU Dual Bank.pdf

## Setup

1) The demo uses the **NUCLEO-H563** (using STM32H5 MCUs) and 2x USB Cables.
Connect STLINK USB conenctor of the Nucleo board to the Host.
2) With Teraterm (or similar Terminal Software), connect to STLINK Virtual COM port of the Nucleo board (baud rate@115K & no parity) to view printf messages fromcode. 
3) Using STM32CubeProg (with STLINK connection mode) do a full erase of the chip.
4) Using STM32CubeProg (with STLINK connection mode) check that SWAP_BANK bit is reset (not checked) in the User Configuration option Bytes.
5) Program STM32H5_USB_DFU_Dual_Bank.bin at address 0x08000000 and 0x08100000 (at beginning of both banks 1 and 2).
6) Connect user USB connector of the Nucleo board to the Host.
7) Reset the STM32H5 on the Nucleo board by pressing reset Button (black button).

Please check the PDF document for more details.

## Application description
The Example code demonstrates the bank swapping mechanism when doing
firmware upgrade of the application code using USB DFU (Device Firmware Upgrade).
The code checks if application code is present at address 0x0802 2000, if there is code it will jump to it.
The code also checks if the user button is pressed after releasing the reset button on the board, if so, it will run the USB DFU code.
The Example shows how to do a firmware upgrade of the application code on the opposite bank of the active one.
The example code shows the swap bank mechanism.

Please check the PDF document for more details.

## Running Demo

1) Status message after reset:
After resetting, the board will boot from Bank 1.
Check Terminal message from the system.
Button is not pressed so it will check if there is an application code in the active bank.
But here it is blank so it will automatically execute USB DFU.

2) Connecting to USB DFU device:
The device is enumerated as a USB DFU device.
Using STM32CubeProgrammer connect to the device using USB as seen here following these steps.

3) Connected to the USB DFU device:
After clicking connect, the STM32CubeProgrammer is now in connected state and we can proceed to do a firmware upgrade.

4) Performing a firmware upgrade on the other bank (bank 2):
Using STM32CubeProgrammer, go to to the "Erasing & Programming" tab. Click on the "Browse" button to point to where the file “Application_Example_for_STM32H5_USB_DFU_Dual_Bank.bin” is located.
For the Start Address input 0x08122000.
Options to be used:
skip flash erase before programming: UNCHECKED
Verify programming: CHECKED
Full Flash Memory checksum: UNCHECKED
Run after Programming: CHECKED

please check pdf document for the options on the screen shot to be sure.

Click Start Programming.

5) Log from STM32CubeProgrammer after firmware upgrade:
Check the different log messages during the upgrade in STM32CubeProgrammer.

6) After the firmware upgrade is done on bank 2:
Check the terminal messages after the firmware upgrade has been performed.
This shows that we are now running from bank 2 because after the firmware upgrade is done, we perform a bank swap.
This shows that in this case the user button is not pressed.
This shows that because an application code was found in the Application code section of the bank 2 that we are jumping to application.
This shows the application code running.

7) Performing a new firmware upgrade:
To do a new firmware upgrade we will hold the user button prior to and after releasing the reset button, this will force the execution of the USB DFU.
Check the terminal messages:
This still shows that the active bank is bank 2.
This shows that in this case the user button is pressed.
This shows that the USB DFU is running.

8) Connecting to USB DFU device:
The device is enumerated as a USB DFU device.
Using STM32CubeProgrammer
connect to the device using USB as seen here following these steps.

9) Connected to the USB DFU device:
After clicking connect, the STM32CubeProgrammer is now in “Connected” state and we can proceed to do a firmware upgrade.

10) Performing a firmware upgrade on the other bank (bank 1):
Using STM32CubeProgrammer, go to the "Erasing & Programming" tab click on the "Browse" to point to where the file “Application_Example_for_STM32H5_USB_DFU_Dual_Bank.bin” is located
For the Start Address input 0x08122000.
Keep the rest of the default options.
Click Start Programming.

11) Log from STM32CubeProgrammer after firmware upgrade:
Check the different log messages during the upgrade in STM32CubeProgrammer.

12) Running demo after firmware upgrade on bank 1:
Check the terminal messages after the firmware upgrade has been performed:
This shows the terminal messages after the firmware upgrade has been performed.
This shows that we are now running from bank 1 because after this new firmware upgrade was completed, we performed a bank swap.
This shows that in this case the user button is not pressed.
This shows that because an application code was found in the
Application code section of the bank 1 that we are jumping to application.
This shows the application code running.

Please check the PDF document for more details.

## Troubleshooting

**Caution** : Issues and the pull-requests are **not supported** to submit problems or suggestions related to the software delivered in this repository. The STM32H5_USB_DFU_Dual_Bank_demo example is being delivered as-is, and not necessarily supported by ST.

**For any other question** related to the product, the hardware performance or characteristics, the tools, the environment, you can submit it to the **ST Community** on the STM32 MCUs related [page](https://community.st.com/s/topic/0TO0X000000BSqSWAW/stm32-mcus).
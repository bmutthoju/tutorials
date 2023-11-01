# ARM Cortex M Microcontroller DMA Programming Demystified #
## Section 1: DMA Getting Started and Multi AHB Architecture ##
### About the Instructor ###
### Course Overview ###
1. Multi AHB Architecture - important for understanding DMA
	1. Backbone behind master/slave communication
	2. MCU block diagram
	3. Multi AHB Bus matrix
	4. How ARM can DMA can concurrently talk to different slaves
2. Section 2-4:
	1. Step by step procedure to install IDE
3. Section 5:
	1. Installing STM32CubeMX
4. Section 6:
	1. GPIO Led Toggling using polling & interrupt in DMA mode
5. Section 7:
	1. UART (SRAM to UART in interrupt mode)
6. Section 8:
	1. DMA functional block diagram
		1. Streams
		2. Channel mappings
		3. FIFOs
		4. ...
7. Section 9:
	1. ADC
		1. ADC to SRAM data transfer
		2. How it works with DMA
8. Section 10:
	1. DMA arbiter and stream priority
9. Section 11:
	1. Transfer modes
		1. Peripheral to memory and back
		2. ...
10. Section 12:
	1. DMA application from scratch (without STs software)

### FAQ ###
1. Board:
	1. STM32 Nucleo64 F446RE
	2. Any (Discovery, ...)
2. OS: Windows/Mac/Linux
3. IDE: KEIL-MDK-5 for windows, openSTM32 System WOrkbench for Windows/Linux/Mac

### Source Code ###
1. [https://github.com/niekiran/DMAProgramming](https://github.com/niekiran/DMAProgramming)

### Important Note ###

### DMA Introduction: Master - Slave Communication ###
1. Master-Slave communication

		ARM C4 <->| |
		          | |<-> Memory
				  | |
				  | |<-> ADC (Analog to Digital) (Input)
				  | |   [DR - Has data]
		UART <--->| |
		          | |
				  
	1. Alternative 1: ARM CM4 runs LDR command to load into register and STR to transfer from register into memory
	2. Alternative 2: Why can't ADC push the data into memory?
		1. Not possible
			1. ADC doesn't come with intelligence to generate bus transactions and control signals to move data from one location to another
				1. Example: LDR - Processor decodes the instruction and actuates many control signals
					1. Generates Bus transactions
						1. Processor knows how to get control of the Bus but ADC cannot take control
		2. **Anyone who can take control of the Bus and generate Bus transactions to move data from one place to another are called Masters (Bus Master say)**
			1. Example: ARM is Bus Master
		3. **Anyone who cannot take control of the Bus is called a slave**
			1. Example: ADC
			2. A slave can only generate asynchronous events to indicate to the processor that it has data (interrupts)
		4. **Can we offload the task of data transfer from processor to someone else? To whom?**
			1. Solution: **DMA Controller**
				1. It is also a master
				
						ARM CM4 <->| |
						           | |<-> Memory
						DMA Co <-->| |
						           | |
						
					1. **DMA Controller has intelligence to generate transactions to take over the Bus to move data without taking the help of ARM**:
						1. Peripheral to Peripheral
						2. Peripheral to Memory
						3. Memory to Peripheral
						4. Memory to Memory
					2. **DMA doesn't execute instructions**
						1. It only has logic to take over bus and do data transfer
				2. Where is this useful?
					1. Example: Consider ADC and UART
						1. Let us say ADC has generated data and is stored in its register
						2. Let us say UART is also receiving data from the external world
						3. When UART receives data, it triggers an interrupt to the ARM
						4. If priority of UART is greater than ADC, it will be served
							1. We need to raise priority of UART (not fully solved)
							2. Solution 2: Make UART trigger interrupt to DMA controller
								1. **DMA controller copies data directly from UART to Memory** (ARM is not required)
									1. Design: Using DMA is a choice
					2. Advantages:
						1. Saves power consumption:
							1. ARM otherwise needs to spend a lot of bus cycles in LDR and STR
								1. Requires decoding engine and other engines of the processor to be on
							2. **DMA controller consumes lower power as compared to ARM**
2. Masters:
	1. Multiple DMA controllers
	2. Ethernet controller
	3. USB controller
	4. ...

### Understanding MCU Block Diagram ###
1. Download STM32F446xC/E datasheet
2. Block diagram:
3. Reference manual
	1. Memory and Bus Architecture > System Architecture
		1. 7 masters
			1. ARM Cortex M4 (AHB port controllers)
				1. I-Bus (AHB Bus Master)
				2. D-Bus (AHB Bus Master)
				3. S-Bus (AHB Bus Master)
			2. DMA1 memory bus (Peripheral Bus & Memory Bus Controller)
				1. Controlls AHB master ports
			3. DMA2 memory bus (Peripheral Bus & Memory Bus Controller)
				1. Controlls AHB master ports
			4. USB OTG HS (High Speed)
		2. 7 Slaves
			1. (Peripherals hanging on APB 1 and APB 2 bus and the buses are connected to the main bus)

### Understanding Multi AHB Bus Matrix ###
### Concurrent Data Transfer using ARM and DMA ###
### Concurrent Data Transfer using ARM and DMA-Demonstration ###
### Concurrent Data Transfer using ARM and DMA-Demonstration contd ###

## Section 2: Development Board Used in our Courses ##
### Note for the Students ###
### About MCU Development Board ###
### STM32F4 Discovery and Nucleo: Board Details ###
### ST-Link Driver Installation ###
### ST Link Firmware Upgrade ###

## Section 3: Keil-MDK-5 Setup for ARM Cortex M based MCUs ##
### Note of the Students ###
### KEIL-MDK-5 Installation ###
### KEIL-MDK-5 Installation Contd ###
### KEIL-MDK-5 Pack Installation ###
### Locating Pack Installation Files ###
### Creation of a KEIL Project ###
### Exercise: LED Toggling App using Board BSP APIs ###
### Exercise: LED Toggling App using Board BSP APIs-Nucleo ###
### Exercise: Adding Button Support Using Board BSP APIs (Nucleo) ###

## Section 4: Installation Open STM32 System Workbench ##
### Downloading OpenSTM32 System-Workbench ###
### Installing OpenSTM32 System-Workbench ###

## Section 5: STM32Cube Mx Installation and Code Generation ##
### Note for the Students ###
### STM32CubeMX Installation ###
### Creation of Projects using STM32CubeMX Part-1 ###
### Creation of Projects using STM32CubeMX Part-2 ###
### Creation of Projects using STM32CubeMX Part-3 ###
### Creation of Projects using STM32CubeMX Part-4 ###

## Section 6: DMA Exercises: GPIO Polling and Interrupt ##
### DMA Programming: Generic Steps to Follow ###
### Toggling of LED using DMA (Polling mode) Part-1 ###
### Toggling of LED using DMA (Polling mode) Part-2 ###
### Toggling of LED using DMA (Polling mode) Part-3 ###
### Toggling of LED using DMA (Polling mode) Part-4 ###
### Toggling of LED using DMA (Interrupt mode) Part-1 ###
### Toggling of LED using DMA (Interrupt mode) Part-2 ###

## Section 7: DMA Exercises: UART to SRAM ##
### UART to SRAM Data Transfer using DMA (Interrupt Mode): Big Picture ###
### UART to SRAM Data Transfer using DMA (Interrupt Mode): Implementation ###
### UART to SRAM Data Transfer using DMA (Interrupt Mode) Contd ###

## Section 8: DMA Functional Block Diagram (What's Inside the DMA Controller?) ##
### Master and Slave Ports of DMA ###
### DMA Streams ###
### DMA Channel Mapping ###
### DMA Channel Mapping Case Study 1: P2M ###
### DMA Channel Mapping Case Study 2: M2M, M2P ###

## Section 9: DMA Exercises: ADC to SRAM ##
### DMA Exercise: ADC to SRAM Big Picture ###
### ADC and DMA Configuration Settings ###
### ADC and DMA: Understanding Code-1 ###
### ADC and DMA: Understanding Code-2 ###

## Section 10: DMA Arbiter and Stream Priority ##
### DMA Arbiter and Stream Priority ###

## Section 11: DMA Transfer Modes and FIFO Mode ##
### P2M Data Transfer ###
### M2P Data Transfer ###
### DMA Exercise: SRAM to UART2_TX Part-1 ###
### DMA Exercise: SRAM to UART2_TX Part-2 ###

## Section 12: DMA Programming form Scratch (Register Level Programming) ##
### Introduction ###
### M2P Data Transfer: Project Creation ###
### Button Init Steps to Recieve an Interrupt ###
### Coding for Button Init Part-1 ###
### Coding for Button Init Part-2 ###
### Coding for Button Init Part-3 ###
### Implementing Button Interrupt Handler ###
### Discussing Steps to Configure the UART Peripheral ###
### UART PINMUX Configuration Settings ###
### Code to Bring Out UART TX RX Functionality on GPIO Pins ###
### Setting up Baudrate and Configuring UART Parameters ###
### Testing UART Communication ###
### Brainstorming DMA Initialization Steps ###
### Identifying the DMA Stream ###
### Configuring DMA Stream Direction and Data Width ###
### Configuring Channel Selection ###
### Testing with UART TX DMA Request ###
### DMA Stream Interrupt (IRQ) Discussion Part 1 ###
### DMA Stream Interrupt (IRQ) Discussion Part 2 ###
### Coding DMA Stream IRQ Handler: Part 1 ###
### Coding DMA Stream IRQ Handler: Part 2 ###
### Note for the Students ###

## Section 13: BONUS LECTURE ##
### BONUS LECTURE ###
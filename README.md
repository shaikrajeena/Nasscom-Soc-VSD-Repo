![image](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/adaeb49b-625f-4806-937c-b655ebb225c0)# Nasscom-Soc-VSD-Repo
## VLSI design(SKY130)
//............................................VLSI -CHIP Design document ...........................................................//

### DAY-1:Introduction to open-source  EDA, OpenLANE and SKY130 PDK

## - 1.1.How to talk to computers
   
* _Introduction to QFN-48 package_:

Every board, every electronic circuitry or FPGA board will have the processors. For example, take the below board (ARDUINO).
![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/5429022c-1cbb-4229-aa4c-047b023275cd)

The VLSI industry will work on the inside the highlighted chip(IC). The typical overview of the chip is shown in below diagram.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/7d4b2be7-9e2f-4846-8485-66cf54d3f154)


If we want to design a particular board then the above figure is the block diagram of the particular board. The center one (Highlighted) is processor and along with the processor we have all the interfaces along with that JTAG,QSPI-FLASH ,ADC ..etc is shown in the figure.As we are talking about the chip design, we need to see inside the chip what and all it is containing and how it is desgined. Let’s study about the inside chip in below content.All processors sit in package (there are different types of packages available) the below figure is the example of package: QFN-48. The chip will be sat inside the package and connected with wire-bonds as shown in below diagrams.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/46f7959c-ac96-4a31-b29d-8dbf6d248b99)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/cc9cda51-a355-4d4f-8d76-bede40fe7fe7)


If we open the chip the main part it contains PADS. Through PADs we can send the signals inside the chip or outside the chip. Other part is “CORE” it consists of basic digital logic for example and gate, mux,.etc. If come inside the PADS it consists of all the “foundry IPs”, Where foundry is consists of machines (Where actually chips get manufactured and it is set of machines) where actual chip design/soc design engineers will continuously communicate until the chip manufacturing will be done.IPs are nothing but Intellectual property. Processor will have several IPs, which are nothing but they need some intelligence to build/work particular block (example: UART, I2C,.etc) .where “Macros” are pure digital blocks.The below figure shows the main parts of the inside chips and the foundry IPs and macros are highlighted.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/0ad96f39-e745-49ad-99f7-0c79b027f770)
![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/a71c472c-64bc-4958-8f42-1ecf0cccf267)

* Introduction to RISC-V
The user will write any simple code for example addition of two numbers it should be translated into assembly code when you are compiling. Then by using assembler the assembly language is again translated into the machine level language/Binary language (which includes only 0 &1) . Then those instructions will be passed through the interfaces like HDL (High level description language) to the layout as shown in the below diagram. That is how the program will be transferred from compiling stage to  GDS.
![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/d6d344de-fda1-4b44-8b96-f9e44a06e662)

The below diagram shows how the applications will talk with the hardware. Applications will talk to the system software.which includes mainly OS,compiler & assembler. The main jobs of any OS(windows,linux..etc) are to handle the I/O operations and allocate memory for the instructions/tasks/applications and perform low level system functions. The ouput of the OS which main written in any programming language will be given to the compiler then compiler will generate the instructions based on the architecture it should be like Intel or ARM ..etc . Then those instructions will be given to the Assembler in the form of .exe file then assembler will convert those instructions into the machine level language which includes binary digits 0 & 1.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1bf80f15-8843-4cb3-8589-fe6cf15a3b07)

For example, if we take the application as stop watch the code is written in C language as per RISC-V architecture and those will be converted into the assembly language and then transferred to the hardware as shown in below diagram.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/4ffafb77-64ba-46be-8854-deed8ecc2b3c)

Compiler will generate the instructions by using Abstract Interface it is called the ISA(Instruction Set Architecture). Assembler will convert the assembly code into machine level language then again by using the HDL(hardware description language) it will generate the Synthesized netlist of the RTL then physical design implementation will be created and passed to the hardware as shown in below diagram.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/fcac5af1-0dbc-4bbe-aa66-4a5a1e00a4fb)


##    - SoC Design and OpenLane




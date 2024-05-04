# Nasscom-Soc-VSD-Repo
## VLSI design(SKY130)
//............................................VLSI -CHIP Design document ...........................................................//

# DAY-1:Introduction to open-source  EDA, OpenLANE and SKY130 PDK

## 1.1.How to talk to computers
   
## * _Introduction to QFN-48 package_:

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

 ## *_Introduction to RISC-V_:
The user will write any simple code for example addition of two numbers it should be translated into assembly code when you are compiling. Then by using assembler the assembly language is again translated into the machine level language/Binary language (which includes only 0 &1) . Then those instructions will be passed through the interfaces like HDL (High level description language) to the layout as shown in the below diagram. That is how the program will be transferred from compiling stage to  GDS.
![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/d6d344de-fda1-4b44-8b96-f9e44a06e662)

The below diagram shows how the applications will talk with the hardware. Applications will talk to the system software.which includes mainly OS,compiler & assembler. The main jobs of any OS(windows,linux..etc) are to handle the I/O operations and allocate memory for the instructions/tasks/applications and perform low level system functions. The ouput of the OS which main written in any programming language will be given to the compiler then compiler will generate the instructions based on the architecture it should be like Intel or ARM ..etc . Then those instructions will be given to the Assembler in the form of .exe file then assembler will convert those instructions into the machine level language which includes binary digits 0 & 1.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1bf80f15-8843-4cb3-8589-fe6cf15a3b07)

For example, if we take the application as stop watch the code is written in C language as per RISC-V architecture and those will be converted into the assembly language and then transferred to the hardware as shown in below diagram.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/4ffafb77-64ba-46be-8854-deed8ecc2b3c)

Compiler will generate the instructions by using Abstract Interface it is called the ISA(Instruction Set Architecture). Assembler will convert the assembly code into machine level language then again by using the HDL(hardware description language) it will generate the Synthesized netlist of the RTL then physical design implementation will be created and passed to the hardware as shown in below diagram.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/fcac5af1-0dbc-4bbe-aa66-4a5a1e00a4fb)


###    1.2.SoC Design and OpenLane

### *_Introduction to all the components for digital ASIC design_:
 For designing ASIC we reuired so many elements.Mainly the below three required and shown in the below figure along with open source tools required for each category.
                1. RTL IP's 
                2. EDA Tools
                3. PDK Data

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/7da86cfd-294d-41f3-9074-36ca42807706)

What is PDK ? PDK is nothing but process design kit which actually a interface between the FAB and the designers
which includes collection files used to model a fabrication process for tge EDA tools used to design an IC. All those files may include the below elements        
        
         * Process design rules: DRC,LVS
         * Device models,digital standard cell binaries,I/O libraries
   
   Google designed open source tool as "__SKY WAFER__" for PDK. The tool is desgined for 130nm chips. Which is similar to Intel:P4EE @3.4GHz processor.
   The RISC-V single cycle RV32I design with 327MHz also desinged by using sky wafer tool.The below figure shows the distribution of ICs with different technologies in 2019.
  
   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1d383ac9-90a1-4fc1-83c1-f5fa8eecb3b8)

### *_ASIC-DESIGN FLOW_:

The main objective of ASIC design flow is RTL to GDSII.The simplified RTL flow is illustrated in below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/488fb0db-6780-40c7-9d25-67086d1d5fd4)

###  1._Synthesis_:
It converts RTL to a circuit out of components from standard cell library(SCL) resulted as gate level netlist. Standard cells have regular layout which may have different views and models.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/8478723d-6a3d-48c9-a204-5e835d29933a)

 ### 2._Floor and power planning_:
 It needs to meet different things based on single(macros) component or whole chip. The main object is to plan silicon area and create robust power distribution to power the circuits.          

          1. _Chip floor planning_: Partition the chip die between different systems building blocks and place the I/O pads as shown in the figures.
          2. _Macro floor planning_: It allocates the dimensions, pin locations and rows definitions as shown in below figures
          3. _power planning_: Power network constructed chip is powered by multiple VDDs and grounds(vss) and power pins are connected to multiple components by horizantal or vertical metal straps as shown in below figures to obtain low resistance.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/ddc2920d-93d5-449f-ade0-33bb85a8aecf)


![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1d3a2f75-f76a-43fd-9aea-6579dffdacb3)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/df0b7c6a-a68e-47c6-9c62-b0b50a480ce6)


### 3._Placement_:

Place the cells on the floorplan rows,aligned with the sites to reduce interconnect delay. There 2 steps followed in placement as listed below,
           
            - Global Placement: Optimal positions for all cells which are not legal so cells may overlap       
            - Detailed Placement: Positions obtained are minimally altered to be legal

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1706fe9f-6a39-4bc6-8e97-54c0708b8eb0)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/64f03cb7-81be-4ccf-af21-d8dd65fdad9c)

 ### 4._Clock Tree Synthesis_:

 Before routing the signals we need to route the clocks. Thiis will create a clock distribution network as shown in below figure,Which needs to deliver the clock to all sequential elements(eg.Flipflops) with minimum skew(Zero is hard to achieve). Usually this network will be in good shape usually a tree shape.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/96a0fbc2-f811-4346-b7bd-8f085791be36)

 ### 5._Route_:

Implement the interconnect using the available metal layers  with valid pattern. The metal layers used defined by the PDK which includes the pitch,tracks & minimum width and so many. It uses the divide and conquer approach for routing. two types are followed
        
         - Global routing: Generates routing guide
         - Detailed routing: Uses the routing guide to implement

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/4247324a-a748-4892-acf8-492eef184fbf)

### 6._Sign Off_:

The last stage is signoff which mainly includes two parts 
     
      - Physical verification : Where design rules(DRC)rechecked and Layout vs Schematic(LVS) will be rechecked.
      - Timing Verification : Static timing Analysis(STA)

 ### _Introduction to OpenLANE and strive objects_:

 OpenLane which consists of APACHE 2.0 license.Started as an open-source flow for a true open source tape-out experiment.Strive is a family of open everything SOCs(Open PDK,Open EDA,Open RTL) The main goal of OpenLane is to produce a clean GDSII with no human intervention(no-human in the loop) Clean means NO LVS ,DRC Violations and no timing violations but the timing one is WIP(work in progress). The Strive family and the features and the sponsers is shown in below figure.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/2247cc32-5a6b-4708-8d9c-7657f063118a)

  __OpenLane ASIC Flow__: 


  OpenLane is tuned for skywafer 130nm it have open PDK and also supports XGAB180 & GFB0G .Can be used to harden macros and chips.
  This will work in 2 modes ,

           - Autonomous or Interactive
           - Design space expkoration

   OpenLane is based on several open source projects such as YOSYS,QFLOW,ABC,Fault,OpenRoad & many others. The below figure shows the ASIC flow of openLane.

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/d98bff36-6ee9-4a53-808e-3f2b6e798194)


The Design flow starts with RTL synthesis. RTL is fed to YOSYS with the design constraints.Yosys translates the RTL into logic circuits using generic components.The circuit can be optimized and then mapped into synthesis cells using ABC. Synthesis exploration used to genertae reports which are fed by synthesis strategy.It has design exploration tool used to sweep design configurations and genertae reports this is very useful to choose the best  design configuration among so many and also used for regression testing(CI).OpenLane ran on ~70 designs and compared the results to the best known ones. 

After synthesis testing section will come using DFT(Design for test).Where scan insertion ,fault coverage & fault simulation will be done. and after that physical implementation as discussed in above section with different steps involved in simplified RTL design.

As we can see in the OpenLane ASIC design flow figure shown in above  which involves optimization which involves (LEC) Logic equivalance checking using YOSYS.Everytime the netlist is modified and verification must be performed LEC. Which is used to formally confirm that the function did not change after modifying the netlists. During physical implementation openLane has special step i.e, __Fake ant Diodes insertion__ which will deal with antenna rules violations. When a metal wire segment is fabricated it can act as an antenna. By using OpenLane special feature this will be taken care as below instructions,

          - Add antenna diode cell to leak away charges.
          - Add a fake antenna diode next to every cell input after placement.
          - Run the antenna checker(Magic) on the routed layout.
          - If the checker reports a violation on the cell input pin ,replace the fake diode cell by a real one.

#### 1.3. Get Familiar to Open-source EDA tools

   ####  _OpenLane directory structure in detail_:

Actually OpenLane is not a tool its a flow which acts comprises of many open-source tools out there ex:Yosys. All these tools are inbined with OpenLane flow.This will have the complete RTL to GDSII flow.
For more information about the OpenLane follow the below links,
      1. [Github link](https://github.com/efabless/openlane2)
      2. [Youtube Link](https://www.youtube.com/watch?v=Vhyv0eq_mLU)

   OpenLane is having complete flow from RTL to GDSII . If we open the working directory we can observe the all the folders for each category.There are different PDK files will be available but we need to work on SKY130A PDK. Each PDK folder consists of two types of folders libs.ref & libs.tech folders. libs.ref folder mainly include specifications to the techbology where libs.tech folder include specifications of tools.

Mainly we focus on __sky130_fd_sc_hd__ folder.If we see the abbrevation of the folder name fd means foundry ,SC means standard cell and HD means variant of PDK (which may be high density).

### _Design Prepration steps_ _and_ _Review files after design prep and run synthesis_:

Follow the below steps to open OpenLane and to run the synthesis.
         
         
         - go to openlane directory
         - Type--> docker(Then it will move to bash shell prompt)
         -  Then type -->./flow.tcl -interactive( It will open the OpenLane)
         -  After that type -->package require openlane 0.9(All the required files will be merged here)
         - Then type --> prep -design picorv32a(Preparation will complete in this step)
         - After that review the files by going into /picorv32a/<updated time folder>/runs/ folder
         - Check temp file which consists of merged.lef file(which includes layer level & cell level information)
         - Important file we need to check is config.tcl which will have all the default parameters information.
         - Then type -->run_sythesis

The below figures shows few of the important steps discussed in above section

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1a6cd348-a1b8-4755-965b-6d66372c49da)
 
   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/21ffcc8d-37a6-4152-84db-c871e33f8cc2)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/5ae645c9-bf41-4ca6-96a8-2d9407044827)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e3580096-3cb6-429b-9b96-718e4df38d8c)
   

### _First Task is to calculate the flop Ratio_:

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/ac9d4de5-0b24-4bab-8bc6-109c96b99476)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/c26251f1-fcb1-481d-85d6-df4963aab00d)


   - Number of D-filipflops : 1613
   - Number of cells        :14876

The total flop ratio = Number of D-flipflops / Number of cells = 1613/14876 = 0.108429.. * 100 = 10.842 %

 ### _Flop Ratio is 10.842%_  





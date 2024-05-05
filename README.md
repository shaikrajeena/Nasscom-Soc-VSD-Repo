# Nasscom-Soc-VSD-Repo
## VLSI design(SKY130)
//............................................VLSI -CHIP Design document ...........................................................//

# /////////////DAY-1////////////////// :Introduction to open-source  EDA, OpenLANE and SKY130 PDK

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


 # /////////////DAY-2//////////////////: Good floorplan vs bad floorplan and introduction to library cells

## _2.1.Chip floor planning considerations_:

### _Utilization factor and aspect ratio_:
In physical design the first step is to come up with width and height of the chip. Lets just begin with by taking the basic netlist as shown in the below figure

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/2f2c4035-034e-493a-9043-09f204c067d1)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/de6bc996-f9e8-4eda-9eb7-646da6b9c34f)

Basic netlist is using 2 flipflops(1-Launch FF & 1-Capture FF) and we have simple combinational logic between them. A netlist describes the connectivity of an electronic design.Mostly it will depend on the dimensions of the logic gates and FFs. Lets convert the highlighted symbols into physical dimensions/mostly interested in dimensions of the standard cells not the wires as shown in the below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1d01e8f0-7a5e-4a58-8e23-38bdbff07ad8)

For example, if we consider the height and width are 1 unit & 1 unit as shown in below figure, Then for one standard cell the area will be 1 sq.unit and the area for the flipflops also 1 sq.unit. Now lets calculate the area occupied by the below netlist on a silicon wafer.Remove the wires and place them beside each other as shown in the below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/29ddfd57-5d6b-4e1b-8f31-38fc79b65114)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/5ba058b9-1e1f-4fef-93c5-42fa6c6233ce)

So we need to place the netlist into the core . What is core & die ? 'Core' is the section of the chip where the fundamental logic of the design is placed. A 'die' which consists of core is small semiconductoe material specimen on which the fundamental circuit is fabricated. Okay now how to arrive on its dimensions? Place all logical cells inside the core as shown in figure. The logical cells occupies the complete area of the core as shown in fugure it is called 100% utilization of the core so if we want to add any extra cell it is not possible so always 50 or 60 % of the core will be utilized. If we want to calculate the utilization factor the formula is shown below,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/197e39b8-d95c-4ccd-9235-f6dbc8fabed8)

   Utilization factor = Area occupied by netlist / Total area of the core  

   If we calculate the above diagram utilization factor , 4*1sq.unit /2*2 sq.unit = 1 = 100%

   Aspect Ratio = Height/Width = 2/2=1 --> chip is Square  if aspect ratio other than 1 then chip is rectangular shape.

### _Concept of preplaced cells_:

First of all let us know what are preplaced cells? One Huge circuit is divided into parts as shown in below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/024caf9c-f43a-4568-a25b-312f51b9c532)

The divided parts treated as blocks then extend the IO pins after that black box the boxes which means the netlist will be invisible to the top netlist as shown in the below figure, Those blocks will be implemented seperately so that we can use those blocks repeatedly.Similarly there are other IPs available like memory,Comparator,Multiplexer,Clock gating cell and many other.Theier functionality will be implemented once and used repeatedly.These blocks placement has to be done before routing. These are called the pre placed cells.The arrangement of these IPs in a chip is referred as floorplanning.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/09cbcdc4-3de0-4a50-9229-e0091a0e37fd)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/813b8b5e-177f-448a-b0e0-52a534c7180a)

These IPs/blocks have user defined locations and hence are placed in chip before automated placement and routing are called pre placed cells .automated placement and routing tools places the remaining logical cells in the design onto the chip.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/578eb8e4-341f-4866-9401-4a1ee5766d3d)

For example we have blocks as blocka & block b & block c .so how do how do we defined the locations of pre placed cells? All the blocks placed close to the input side  but it is dependent on the design background the example is shown in the above figure. But the locations of the preplaced cells not touched while go on the design cycle.

### _De-Coupling Capacitor_:
Consider the amount of the switching current required for a complex something like shown in below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/6f194c0d-bcc9-4f6e-b400-8d092013c857)

    1. Consider capacitance to be zero for the discussiob Rdd,Rss,Ldd,Lss are well defined values.
    2. During switching operation,the circuit demands switching current that is,peak current(Ipeak)
    3. Now due to the presence of Rdd & Ldd there will be a voltage drop across them and the voltage at node 'A' would be Vdd' instead Vdd.

Whenever AND/OR gate switches from logic-0 to logic-1 it needs current. Basically small capacitance needs to charge to represent logic 1. The amount of charge will be sent by the supply voltage .Also whenever switching from logic 1 to logic 0 responsibility of the VSS to take that amount of the charge.
But in reality from power supply voltage will flow to the circuit.There is a drop in wire becuase those wires are physical wires which will have physical dimensions(Means they have resistance ,inductance & Capacitance).So multiple voltage drops will be there .so exact voltage required for the transition wont occur.
If Vdd goes below the noise margin,due to Rdd & Ldd the logic-1 at the output of the circuit won't be detected as logic-1 at the input of the circuit following the circuit. The noise margin figure is shown in below,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/697c7ddf-798c-4695-841d-79bf7f08ca11)

We can avoid these noise margins issue by adding decoupling capacitors as shown in below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/845a75f5-6bbd-4405-b0a1-ed0d2f72e3ae)

So the decoupling capacitor will have the same voltage as like power supply so there wont be voltage drops.surround all the pre-placed cells with decoupling capacitors as shown in below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/159670cc-3dad-4916-b7f7-b88ff206d2df)


### _Power Planning_:

Before going to power planning first we need to take care of the local communications.for example lets take one macro will be used repeatedly so there will be particular demand like current is needed for each and every cell of the macro. For example as shown in below figure we have 4 macros used assume one macro is driver other is load.there is a signal given to the load from the driver.(The signal is logic-0 to logic-1) we need to maintain the same signal so that the load receives same signal but problem ariase. Observe the below figure,the red signal dont have de-coupled capacitor the power supply has to supply the current but it is very far from the signal so there will be multiple voltage drops.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e920d3bb-dcc7-4c17-8c1d-f43fbaf00b78)

Just consider the below figure, This means all the capacitors which were charged to 'V' volts will have to discharge to '0' volts,through single ground tap point.This will cause a bump in ground tap point as shown in the figure.The size of the ground bounce exceeds the noise margin it might enter into undefined state.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/8d338a9a-bd39-4ead-9092-4c4ad971f926)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/c0197b34-3716-4b49-b91d-37fd5438357d)

If all the capacitors  charge from logic 0 to logic 1 as shown in below figure voltage droop will occur. 

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/34184950-a95f-4482-bbfb-b53b9e36ddf7)

All these problems are coming just we are using only one power supply the sollution is to keep multiple power supplies as shown in the below figure there wont be voltage drops.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/48bcfdab-dc6f-49b6-b919-918e292ffd90)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/bfe306b8-ba0e-43c2-a562-4dac911e55b9)


### _Pin placement and logical cell placement blockage_:

Lets take the below design for example that needs to implemented there 4 different colours of designs which will be attached with the pre-placed cells as shown in the below diagram,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/3833c1c9-41a0-4311-b292-78b76a529eff)
 
 so we have all the inputs and ouputs as shown in the above figure. Pin placement of the input and output ports will be based on designer perspective but for the below example inputs are placed in left side of the chip and outputs are placed in right side of the chip.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/f85f9c15-9150-4c68-b9b2-85a0e3618819)

 After that logic cell blockage will be added as shown in the below figure.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/281606ef-028d-40ea-95e0-979d0c8ff678)

 Below are the figures from openLane for floor planning practice.

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/ca95e063-6ffb-42a6-b6dd-e5d6ef244d20)

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e549bb3e-4d11-40df-bcc3-1563d8926c35)

#### 2.2.Library binding & placement:

#### _Netlist binding and initial place design_:

The important step is in placement and routing to bind the netlist into physical cells. The exact meaning is for example we take the below figure netlist with all the gates and the shape of those gates represents the functionality of the gate but in reality we dont have like OR gate shape.we have shapes something like box with height and widths.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/c05eb336-8fce-48a7-ac48-49d98051f59f)

The below rectified figure will present in shelf .shelf is called as library.Library not only having all the boxes but also timing information of particular cells.Library classified into 2-types.1-consists of shapes and cells and one might consists of delay information. Library will have height and width of the each and every cell and delay information of each and every cell and delay information of each and every cell plus required condition of particular cell for example at what condition FF emits the output along with all these it also has various shapes of the cells with various flavours of same cells as shown in below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/b5fb5dfc-2816-4733-885b-9191605794b1)

The next step is placement .we have well defined floorplan as shown in below figure,is to place the netlist into the floorplan.Placement step should not touch the pre-placed cell area.By seeing the netlist which ever cell is close to input or output accordingly place those cells inside the floorplan.as hsown in below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/6527f9f3-e81e-4a62-a38b-a551b7f50e29)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/24437587-c484-4e65-9eb1-89c4b9a0f700)

#### _Optimize placement using estimated wire-length and capacitance_:

Problems of placement will be solved by using optimization. This is the stage where we estimate wire lenght and capacitance and based on that insert repeaters.We use the signal integrety concept here.To maintain the signal integrety we need someone at the intermediate steps to reproduce the things that is the concept of repeaters.actually repeaters are buffers that will recondition your original signal make a new signal and which replicate the original signal and send it again but loss of area but we need to retain. based on the frequency,specifications setup timing analysis placement is correct or not we need to check.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/dbc0a1bd-d9bc-41cd-b408-dfa7783da77a)

### _Need for libraries and characterization_:

_Library characterization and modelling_ Here part-1 is the concept and theory. where we can do the NLDM,CLS timing,power and noise characterization. First step is logic synthesis, First we have a functionality coded in RTL.Convert the functionality into a legal Hardware is called logic synthesis.Output of the logic synthesis is arrangement of the gates that will represent original functionality described in RTL code. Next is floor planning and then placement and then clock tree synthesis(CTS) then the second last step is routing. at last we do static timing analysis(STA) its the last sign off step as shown in the below figure. but in all these steps one common thing is gates and cells.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/28eec548-1e2e-44f4-8fda-56ef499d5b70)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/0a606bf6-1130-49f7-befc-81abf2f65e34)

 In OpenLane placement is after synthesis,there are two types of placements one is global level placement and detialed level placement tools are different for both the placements. We need to do the placements like the way there should be no overlap. Run the below command in OpenLane and by using _MAGIC_ tool we can see the placement as shown in below figure,  

    -->run-placement

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/fb948c75-2ca2-4466-87e9-6b0f2e95bee5)

Power distribution network gets created in floor plan itself but in OpenLane it is different it wont create in power distribution post that floor plan before routing we do.

#### 2.3. Cell Design and characterization flows

##### _Inputs for cell design flow_:

Placement and routed of the logic synthesis flow is shown in below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/7dd00eec-b9b8-44e0-9f2c-9eb9e3c07764)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/804dbf7d-cb9a-4e92-95a8-1a42a12d02bb)

As shown in above figure the highlighted standard cells are most important in IC design flow. Those are buffer or FF or inverters.Standard cell is placed in a section called library.In library has got different functionality as well different sizes and flavours as well.

#### _Cell Design Flow_:

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/b0bd168e-d71f-41d8-a52a-467815ff8d9e)

As shown in above figure lets take inverter as a basic cell. Though it is single input cell but for an IC design flow it has alot more to do. Cell design flow mainly include 3 steps,those are listed below as well highlighted in above figure.

         1. Inputs
         2. Design Steps
         3.Outputs

 _1.Inputs_:  Called as process design kits(PDKs) will be get by Foundry that will include DRC & LVS rules,SPICE models,Library and user defined specs.DRC is typically rules has to be follow example is illustrated in below figures, Coming to SPICE models it consists of threshold values of voltage and current and lot more . 

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/cd04f0fe-0752-41de-a642-d8cf84bc9f96)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/f1212b24-015f-4518-890b-5ec4da229721)

For example as a user defined specification  if we take one circuit outputs cell height is defined by the seperation of the power and ground and cell width is depends on the timing information.another example is supply voltage as illustrated in below figures,

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1a259c93-2509-4a38-898f-d58c27b1eafc)

 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/3e3a0f41-4eca-43de-a48f-f02eab42b364)

  2._Design Steps_: There are 3 steps in the design steps those are listed below,

        1. Circuit design
        2. Layout design
        3.Characterization

   All the 3 steps are illustrated in below figures,

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/70fca011-7b63-4b4f-85eb-acadfc4d962a)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/56e6a0fb-8c72-4ee1-a2f2-53ef84f89c38)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e3ecbfa0-6a86-4c51-8012-18c4f61603f7)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/2301f60b-3920-40d0-a272-fb1973af96d1)

   ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/41391567-70b4-4c98-969a-522ecec2ffb3)

    In layout design we need to get the Euler's path traced only once as shown in the above figure.Based on Euler's path need to draw stick diagram as shown in the above figure. Then convert stick digaram into a layout while we adhere to all the DRC,LVS rules and also user defined specifications. By using "_Magic Tool_" we can able to see the layout. Then the final step is to extract the paracitics out od the layout and characterization interms of timing. The output of the circuit design is CDL(circuit description language) and the output of the layout is GDSII(Typical layout file),LEF(Widht & height of cell),Extracted spice netlist(.cir)

   3._Characterization_: Where the outputs are timing,noise,power .libs and functions

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e06208f1-3c46-40d3-80b5-10f626c6f9d2)


#### _Typical Charactarization flow_:

 For charactarization we need to follow certain steps those are listed below,
    
     1. Read the model Files
     2. Read the extracted spice netlists
     3.Recognize the behaviour of the buffer
     4.Read the sub circuits of the inverter(As we are taking inverter as an example)
     5.Attach the necessary power sources
     6.Apply the stimulus(There are different stimulus types available)
     7.Provide necessary output capacitances
     8.Necessary simulation command

All these steps are illustrated and highlighted with the numbers in the below figures, Then the next step is to feed in all these inputs from 1-8 steps in the form of the configuration file into a characterization software called GUNA  this also highlighted in the below figure.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/e43422cd-6ff4-4061-9fe4-07a8671c472b)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/5cca94c3-bde6-4916-8fb9-a665bae61fe5)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/a55e928f-6dcb-4015-95bd-58d90cb93074)

#### 2.4 General Timing Characterization parameters:

 #### _Timing threshold definitions_:

As discussed above in the 6th step where we will apply the stimulus there are various timings we need to follow those are called timing threshold definitions as shown in the below figure,

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/be882e10-6059-4346-a08b-8661f9b02cf2)

All these definitions are important, we see the one of the parameter as slew low rise threshold taken the waveforms from the output of the 1st inverter wheich is given to the second Flipflop input which is close to zero power supply. as shown in the below figures only few are listed.

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/fffde4b9-9aff-4cc8-b663-0a3e86057161)
 
 ![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/0f87374f-8853-418d-a808-6e92e2f87008)


 #### _Propagation Delay_: 
  It is very easy to obtain but if  we cannot taken care it may lead to unexpected reasons. As shown in the below figure if we have both input and output rise and fall threshold for propagation delay we just need to subtract from  "_out-in_"

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/f4b989f4-5acf-4728-a002-ea04c44b0778)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/f752dc98-8922-4b1a-9ecd-e57787c96bc3)

The below figures shows the timing characterization for transition time 

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/1686d1cb-2ed7-44a0-ab76-e6068ff39d7b)

![alt text](https://github.com/shaikrajeena/Nasscom-Soc-VSD-Repo/assets/163321148/b31414ee-21fe-46cc-9a60-f9ea336b4adc)



















 

 

 







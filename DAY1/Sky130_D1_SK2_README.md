# SKY130_D1_SK2 - SOC Design and OpenLANE
  ## Introduction to all components of open-source digital ASIC design


  Desigining the ASIC design in automated way requires several things.  
  
  **Hardware description languages**  
  **CAD Tools**  
  **PDK Data (Process design kits)**    
 	
 #### * Hardware description languages  
 
 It is a specialized computer language used to describe the structure and behavior of electronic circuits.  
 There are 100's of RTL designs over the internet. Here are the some sites.
 #### * PDK

 The interface between the designers and Foundries becomes the set of data files or documents.
 This set of files is called Process Design Kit.
 This PDK includes collection of files used to model a fabrication process for the EDA tools used to Design and also
 Process design rules , Device Models, Digital Standard cell libraries, I/O libraries etc..
 
 June30, 2020 Google released the first ever open source PDK.
 This PDK has its own information to design succesful ASIC using open source.
 
 #### * CAD Tools
 
 CAD tools came as a powerful technology that empowers engineers to create highly complex and efficient integrated chip designs.  
 Mianly Used to automate the design.
 
##  Simplified RTL2GDS Flow.

   ASIC Design is very tough process that involves many steps. A Methodology is needed to make a succesfull ASIC design. The methodology is implemented using the certain flow.


### --> Synthesis

Synthesis is a process of converting RTL code into gate level netlist.

**Synthesis flow**

1.Read the inputs    
2.Elaborate -Translate the RTL code into gtech cells that are technology independent.    
3.Compile- Generate a netlist mapped to a specific library using command compile_ultra. During the compile ,we add the ICG(integrated clock gating)cells whose information is already provided in the RTL.     
4.Optimization-optimize the design such that it meets the area, power and timing specifications. Synthesis tool give high priority to timing over area and power constraints.     
5.DFT(Design for testability) - perform scan insertion in the optimized design.    
6.Generate output.    

Library building blocks of cells have regular layouts.

Typically the standard cell height is fixed rectangular shape but the width is variable for discrete.

### --> Chip Floor Plan

**Floor planning is the art of any physical design. A well and perfect floorplan leads to an ASIC design with higher performance and optimum area.  
Floor planning can be challenging in that, it deals with the placement of I/O pads and macros, the rows on the routing track will define as well as power and ground structure.**


### --> Power Plan

**Power planning is done to provide uniform supply voltages to all the cells in design the primary objective of power planning is to ensure that all on chip components like blocks, memory, IO cells etc have adequate power and ground connections. there are three levels of power distribution that,   
Rings carries VDD and VSS around the chip.      
Straps carries VDD and VSS  from rings across the chip.     
Rails carries VDD and VSS to the standard cell of VDD and VSS.**    

Such parallel structures of power straps mean to reduce the resistance and IR drop and  to address the Electro migration.
Typically the power distribution network uses the upper metal layers because these metal width's are high compare to lower metal layers.
If width will be more the resistance will be less.


### --> Placement

**Placement is the process of placing the standard cells in the design and also Optimizes the design and determines the routability of the design.**

Typically placement is done in two steps

**Global placement followed by detailed placement.**

Global placement tries to find the optimal positions for cells, such positions are not necessarily legal. so cells may overlap or they may avoid rules.  
Detailed the positions obtained from global placement are minimally altered to be legal.

### --> CTS Clock Tree Synthesis

**CTS is used to connect the External Clock to the all internal clock pins of a flipflop. And also inserting a buffer or inverters to all the clock paths in a design to balance the skew.**


### --> Routing

Signal routing

**Routing is the process of creating physical connections based on logical connectivity in the netlist file.**

The router uses the available metal layers as defined in the PDK. The PDK defines thickness, pitch , and min width of each metal layers and also defines vias.
The SKYwater PDK defines its routing layers , lowest layers are Titron nitrate layers, and the following 5 layers are aluminium layers.

Most Routers are Grid based routers.
They first construct the routing grids out of the metal layer tracks.
if the routing Grid is Huge then they will follow Divide and conquer method to route the metal laers.


### --> Sign off

#### * DRC (Design Rule Checking (DRC)):

DRC involves verifying that the layout design conforms to the geometric design rules specified by the semiconductor fabrication process. These rules define minimum widths, spacing, overlaps, and other layout parameters necessary for successful manufacturing. DRC ensures that the design does not violate these rules, which could lead to defects during fabrication.

#### * LVS (Layout vs. Schematic Checking) :

LVS compares the layout design (physical representation) of the circuit with its schematic (logical representation). It verifies that the physical layout matches the intended circuit connectivity specified in the schematic. LVS ensures that there are no errors such as missing connections, shorts, or open circuits that could affect the functionality of the IC.


#### * STA (Static timing analysis)

It is a method of validating the timing performance of a design by checking all possible paths for timing violations.
The main goal of static timing analysis is to verify that despite these possible variations, all signals will arrive neither too early nor too late, and hence proper circuit operation can be assured. Since STA is capable of verifying every path, it can detect other problems like glitches, slow paths and clock skew.

## Introduction to OpenLANE detailed ASIC Design flow
OpenLANE is based on several open source projects. such as below

**RTL synthesis**

RTL is fed to **yosys** with the design constraints yosys translates the RTL into logic circuits using engineering components this ckt can be optimized and mapped into cells in standard cell library using **ABC**, this ABC has to be guidedduring the optimization.

The different designs can use different stratergies to achieve the design targets , for that we have **synthesis exploration** that can be used to generate the report, that shows how the design delay on the area.


Also OpenLANE has **design exploration** utility which can be used to sweep design configurations.
we have 16 configs , the report is looks like below,  
This report is very useful to find the best config for OpenLANE.

**DFT (Design for Testablility)**

After fabrication we can enable this to test the device. This step add extra logic to the ckt without modifying the original functionality.


**Physical implementation**

It includes several steps, all of them are doing by **openroad**.


**LEC**
If they are not equivalent, eventually the optimization is something wrong.
 
During physical implementation we have a special step that is Fake antenna diodes insertion.

This is required to address the antenna diode violations.
# SKY130_D1_SK3 - Get familiar to open-source EDA tools
## Topics to be covered**
**--> OpenLANE Directory structure in detail.**  
**--> Design preparation step.**  
**--> Review files after design prep and run synthesis.**  
**--> OpenLANE project Git link description.**  
**--> Steps to characterize synthesis results.**  

## OpenLANE Directory structure in detail  

The tool which we will be working is OpenLANE,  OpenLane is a not a tool, it is basically flow  which compraises of many open-source EDA tools.
OpenLANE is used to produce RTL2GDS.

Open Terminal and change directory to Desktop.  
To go to openlane_working_directory run the below commands. Openlane_directory has following 3 folders. 



To see what is inside the PDKS folder, run the below commands.  
Many PDKs are very compatible, and they are made to work with commercial EDA tools, not for open EDA tools. The given open_PDKs are found to mitigate this issue. These PDKS having set of scripts to convert these foundries to be compatible with the open-source EDA tools.  
The given Sky130A is a PDK which is made to be compatible with the open-source EDA tools.



If we go to inside the Sky130A folder , two files will be there.  
libs.ref -- It is specific to Technology/Process  
libs.tech -- It is specific to tools,It shows what are the tools are available, we can see below  

libs.ref contains many technology files but we will be working with **sky130_fd_sc_hd**



If we go inside this **sky130_fd_sc_hd** , It will show all design related files. we can see below and also each individual file what it contains  

techlef file will mainly provide metals information.   
lib file will mainly provide timing and PVT corners information.



Till now we see the design related files and it's information.

Now we will go to actual platform OpenLANE.  

To go to openlane run below commands.  

Here flow.tcl will tell how the flow has to go.  
Interactive session means it will execute step by step. To know at which step what is going on and to compare the results from each step we will provide this interactive. If we miss this interactive command It will run complete flow

![Screenshot 2024-03-15 185247](/DAY1/assets/sk1.jpeg)

After this we would require to input all the packages that are required to run this flow.
      

![image](/DAY1/assets/sk2.jpeg)

## Designs folder  
Now the question is what design we have to run?

All the designs that are being run by openlane that are extracted from the design folder. openlane has close to around 30-40 designs. we can see some of the designs below 
Here we will be working with the design **picorv32a**

![g9](/DAY1/assets/sk2.jpeg)

Now lets see the contents in the design **picorv32a**, there will be mainly 3 folders. we can see here.

![g10](/DAY1/assets/sk3.jpeg)

**src** - It is a source file. It provide the verilog file it represents the RTL. and also SDC file.  
**sky130A_sky130_fd_sc_hd_config.tcl value**  even if we don't have this file the flow doesn't affect.  


**config.tcl** - It bypasses any configuration that has been already done in openlane means many switches use a default value that is already there in openlane.  
If we open this config.tcl file , it will show some information like default clock period. 

)

The precedence of how the the openlane takes the values.  
**1. default value which is already set in openlane**  
**2. config.tcl value**  
**3. sky130A_sky130_fd_sc_hd_config.tcl value**  
config.tcl value will overwrite the default value and then sky130A_sky130_fd_sc_hd_config.tcl value will overwrite the config.tcl value.

Lets go back to openlane prompt, The first step is **Synthesis**, but before going to the synthesis stage we need to prepare file system or design setup which will be setting up the data for our design.

-- Go to picorv32a ----> In this for the time being we just have 3 files.  We need to setup the file system to the each and every step of the flow. we will be fetching files for particular location . That location needs to be created. This is called the design setup stage.    

![image](/DAY1/assets/sk4.jpeg)

Here we can see somewhere merging files is complete that means it will merge the lef and tlef files and will provide only one file that is merged.lef.  
Why it is merging these files? Because when we run openlane it need to go to two different location to fetch the lef information and layer information.

**With this, the design setup is completed**

Next, Before we run the Synthesis step we need to chek if anything new was created in our design directory. For this run below commands. **runs** folder was created. go inside that and follow the commands shown below.


![image](/DAY1/assets/sk3.jpeg)

merged.lef contains all cells and layers information. 
If we go inside each folder in the date folder contains, we can see below  

Here one more config.tcl is present. it can be little bit confusing when we see a multiple of config.tcl files one is in design folder and one is in runs folder.
In this config.tcl file - It shows which all default parameters is being taken by the run. some of the information in this config.tcl is ,

![image](/DAY1/assets/sk5.jpeg)

one good thing about openlane is we can make changes on fly. when we make the change and run the step.. EX:- If we made a change belongs to core utilization in the floorplanning inside the original config.tcl and after that we run floorplan. Then that number would be updated here in this config.tcl. So thay way we can check whether the modifications we have done in flow is being correctly reflected in the execution or not.


Now lets go to the openlane prompt , run the command **run_synthesis**  

![image](/DAY1/assets/sk5.jpeg)

![image](/DAY1/assets/sk6.jpeg)


![image](/DAY1/assets/sk7.jpeg)


### Calculation of the Flop Ratio  =  No.of D flipflops/ Total no. of cells

![g19](/DAY1/assets/sk8.jpeg)

we can see report also
**1-yosys_4.stat_rpt** this gives actual synthesis report.

![image](/DAY1/assets/sk8.jpeg)


How the results are populated in the runs folder? If we go inside the results we will see synthesis folder. if we open that it should have synthesized netlist. **synthesis.v**
we can check inside this netlist .all the mappings have been done.




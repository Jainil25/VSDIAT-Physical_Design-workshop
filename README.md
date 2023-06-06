# VSDIAT-Physical_Design-workshop

VLSI System Design Corporation is hosting the "Advanced Physical Design using OpenLANE/Sky130" workshop. In this, we used "Google-Skywater's Opensource 130nm Process Design Kit (PDK)" to build GDSII from the RTL netlist for the PicoRV32a SoC design with Openlane flow. We developed and described our own standard cells using the Sky130 PDK variant. The entire RTL2GDSII flow is automatically executed by OpenLANE. For better timing, timing analysis and optimisation are conducted. Design rule checks are performed as well.
# Contents:
# Day 1

The process of turning a gate level netlist into a physically lay-out that can be manufactured is known as physical design. Initial design partitioning is followed by floor/power planning, standard cell placement, clock tree synthesis, and routing. These will be explained further.

## Talking with computers
### QFN-48 Package and Foundry IPs
The term "QNF-48" is frequently used in the semiconductor industry to describe a particular kind of integrated circuit package. "QNF" refers for Quad No-Lead Flat Package, and "48" represents the quantity of pins or terminals on the package. Due to their tiny size, high pin density, and efficient thermal design, QNF-48 packages are popular for use in a wide range of applications where space is at a premium, including mobile devices and small form factor electronics.

Intellectual Properties (IPs) from semiconductor foundries are pre-designed, pre-verified functional building components. These IPs contain widely used parts that can be included into unique semiconductor designs, such as CPUs, memory controllers, interfaces, and other building blocks. Foundry IPs frequently come with thorough documentation and verification to assure compatibility and stability and save time and effort when compared to building complicated functionality from scratch.

In the context of integrated circuit design, Macros are prefabricated circuitry building blocks that have a defined purpose. Macros are full subcircuits or subsystems that have undergone independent design and verification. As they are simple to integrate into bigger chip designs, they are frequently employed to implement capabilities that are common, like memory arrays or specialised processing units. For complicated semiconductor products, macros can dramatically shorten the time to market and speed up the design process.

By offering pre-designed and well tested components that are simple to include into custom chip designs, foundry IPs and macros both help to efficiently design and produce integrated circuits. They enable semiconductor businesses to concentrate on their distinctive value-add and market differentiation while also reducing design time and enhancing dependability.
### Risc-V
We may communicate with computers by using RISC-V, an open instruction set architecture. A computer programme is first translated to its equivalent Assembly Language Programme, which is nothing more than the conversion of Hexadecimal code, using a RISC-V Assembly language programme. From there, the binary language of 0s and 1s is created. And these 0s and 1s are nothing more than digital signals that can be used in hardware/layout. A HDL code or RTL code that implements the RISC-V architecture and from which the real layout can be mapped serves as an intermediate step between this conversion.

![243388287-47c315a7-20f0-47d3-b9ce-bf95fb704aa6](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/5e2e4306-27e8-4468-8c38-817fb0c952e7)


## SOC using OpenLANE
Digital ASIC A design process that is automated needs a number of components. The components are:

EDA Tools
RTL (Hardware Description Language) Models

PDK Data

Let's discuss PDK data.

PDK data (Process Design Kit): We require a set of files in order to simulate a fabrication process for the EDA tools. These are a part of the kit. It serves as the link between the fabrication team and the designers. Design guidelines, Device models, Digital Standard cell Libraries, I/O lib, etc. are all included in PDK.

Google and Skywater collaborated on an agreement to open source PDK for Skywater's 130nm technology. The first ever openssource pdk was issued by Google. The pdk solely contains data information needed to implement an ASIC successfully using openroad or ocla tools.

Few Opensources for these three components are:

RTL Designs :

librecores.org

opecores.org

github.com

![l1new](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/8e158ad2-2a4c-4d6a-87a4-5a9875845f0e)


EDA Tools :

Qflow

OpenROAD

OpenLANE

PDK DATA

Google +skywater 130nm

## RTL to GDS2 flow 
Synthesis involves leveraging common cell libraries to translate RTL into a gate level netlist.

Floor planning and power planning are used to locate macros and I/O pins according to the size and form of the die. Power is dispersed evenly through the grid's rings, stripes, and rails. Because they are wider and hence have less resistance, upper metal layers are employed for power routing to prevent IR drop and electron migration.

Placement: Cells are placed in their appropriate locations and may overlap according to the netlist through coarse placement. Therefore, we carefully position objects to prevent overlapping and flip them to conserve site row space.

Building a clock tree so that each clock pin of a sequential block is reached with the minimum amount of skew and insertion delay is known as clock tree synthesis.

Synthesis involves leveraging common cell libraries to translate RTL into a gate level netlist.

Floor planning and power planning are used to locate macros and I/O pins according to the size and form of the die. Power is dispersed evenly through the grid's rings, stripes, and rails. Because they are wider and hence have less resistance, upper metal layers are employed for power routing to prevent IR drop and electron migration.

Placement: Cells are placed in their appropriate locations and may overlap according to the netlist through coarse placement. Therefore, we carefully position objects to prevent overlapping and flip them to conserve site row space.

Building a clock tree so that each clock pin of a sequential block is reached with the minimum amount of skew and insertion delay is known as clock tree synthesis.

After routing, we conduct verification during signoff.

Design rule checks (DRC): This type of physical verification ensures that our design complies with design rules. (carried out by MAGIC) Checks whether our layout corresponds with the netlist schematic using the LVS method.(NETGEN AND MAGIC)
Verification of timing: Static Timing Analysis: Verifies that our design complies with all timing requirements and is operating at the specified frequency.

## Introduction to OpenLane and Strive Chipset
Users generally face quite a few challenges when using open source EDA, problems like missing EDA tools for some steps, calibration or tool qualifications are some challenges faced.
Openlane, an open source EDA, is a comprehensive end-to-end solution for rtl2gds flow that consists of many phases and optimised flow. The striVe series of open access chips is available from Efabless. It is a full-featured chipset with open access, open PDK, open RTLs, and open EDA for everything.
The primary objective of the OpenLane programme is to automatically build a GDS2 file without human intervention, and the die that is produced must be clean.

There shouldn't be any LVS infractions on the chipset.

There shouldn't be any DRC infractions on the chipset.

There shouldn't be any timing issues with the chipset.

## OpenLane ASIC Flow
As mentioned, Openlane is an open-access, full-service EDA system that may be used to toughen chips or macros. OpenLane operates in two different ways:

Push-button flow, automatically created GDS2; autonomous.

Interactive: This flow is more carefully planned out and implemented step by step.
![openlane-flow](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/4fbb5203-0b64-42a3-8516-cf9e19e154b9)


The Design Set Exploration function of Openlane allows it to identify the ideal set of parameters and constraints that can be applied to the flow. It basically runs through many configurations and recommends the best option to be utilised as flow limitations.

The flow starts with RTL synthesis and ends with final layout in the GDS format. OpenLANE is based on several OpenSOurce projects such as:

OpenROAD

Magic VLSI Layout Tool

QFlow

ABC

Fault

KLayout

Yosys

OpenROAD App -
OpenRoad app is automatic placement and routing tool and it performs the following function –

Floorplanning

Powerplanning

Placement: Global and Detailed

Post Placement Optimization

Clock Tree Synthesis

Routing: Global and Detailed

### Logic Equivalence Checking –
To determine whether altering the design has had any impact on the chip's functionality or not, LEC must be carried out after carrying out a number of iterations

### Antenna Rule Violation –
A metal wire segment that has been constructed and is long enough can function as an antenna. It can destroy our transistor during manufacture if charge builds up on it. The task of the router is to limit the length of the wire.

We used OpenLANE in a preventative manner. When placing the cells, we made a fake antenna diode and positioned it next to each one. Replace the fake with the genuine one when Magic checks the routed layout for antenna checkers and reports a violation on a cell input pin.

Signoff in openLANE STA is done by openSTA

physical signoff consists of LVS and DRC.
DRC and spice extraction from layout are done via magic.
Magic and Netgen are used for LVS
extracted spice by magic vs verilog netlist

## Lab-Day 1
The directory which we will be using for entire implementation: 
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane
Next up is pdks
Foundary files are made compatible only with commerical EDA tools. OpenPDKS has mitigated ths issue by implementing scripts and files that convert these foundary level PDKS to be compatible with OpenSource EDA Tools.

In pdks directory .we have one of such variant file sky130A
WE will be using sky130_fd_sc__hd, where:
fd = foundry name of skywater
sc = standard cell
hd = high density

To get started, we need to type the following commands(one by one) in /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane 
docker
./flow.tcl -interactive
package require openlane 0.9
This will launch OpenLANE successfully
![Initialise OpenLANE](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/8185017d-a4be-4af2-9fb1-cab0c46d16f5)

now if we will create a design by typing:
prep -design picorv32a
This will create a sub folder named "runs" with the date when this command was executed.
![prep -design](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/e1d6c637-bd0c-4b51-93e7-e4b0396f443f)

Here's an image which displays contents of some important directories discussed above:
![picorv32a contents](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/ad483a36-6ffa-415a-bf97-794d97e7c88e)


Now we can use run_synthesis
![run_synthesis](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/9360dcc4-0563-40e9-9631-53ed24e12509)

after synthesis, we can have a look at the at the statistics report to calculate flop ratio. It is defined as:
flop ratio = no_of_flops/no _of_cells
![yosys_dff stat](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/805bd461-9032-4432-93f3-bebf80bb0ad5)

flop ratio(in my case is): 1613/18036 = 0.08943.

# Day 2: Good vs Bad Floorplan and Library cells

## Floorplan stage

Find height and width of core and die:

Core is where the logic blocks are placed and thus seats at the centre of the die. The dimensions of each standard cell on the netlist determine the width and height. Utilization factor is area occupied by netlist divided by total area of the core. Utilisation factor in a real-world scenario is between 0.5 and 0.6. This is space occupied by netlist only, the remaining space is for routing and more additional cells. Only an aspect ratio of one will result in a square-shaped core because aspect ratio is defined as (height)/(width) of core.

Preplaced cell:

These are reusable complex logicblocks or modules or IPs or macros that is already implemented (memory, clock-gating cell, mux, comparator...) . The placement on the core is user-defined and must be done before placement and routing (thus preplaced cells). The automated place and route tools will not be able to touch and move these preplaced cells so this must be very well defined

Decoupling Capacitors:
Surround preplaced cells with decoupling capacitors. The intricate preplaced logic block needs a lot of current from the power supply to switch the current. However, due to the resistance and inductance of the wire, there will be a voltage drop because of the distance between the main power supply and the logic block. The voltage at the logic block may then no longer fall within the noise margin range (logic is unstable) as a result of this. Utilising decoupling capacitors close to the logic block will provide the necessary current for the logic block to switch inside the noise margin range.

Power planning:
The creation of a power grid network to evenly distribute power to every component of the design is known as the power planning process. This process addresses the unwelcome voltage drop and ground bounce. The metal wires that make up the power distribution network have a resistance that results in steady state IR Drop. Stable-state IR Drop lowers the voltage differential between local power and ground, which lowers the speed and noise immunity of the local cells and macros.

Pin placement: 
The position of the pin affects the timing delays and the number of buffers required, so pin placement is critical in floorplanning. Pin placement options include equidistant placement and high-density placement.

### Placement is done on two stages:

Global Placement = placement with no legalizations and goal is to reduce wirelength. It uses Half Perimeter Wirelength (HPWL) reduction model.

Detailed Placement = placement with legalization where the standard cells are placed on stadard rows, abutted, and must have no overlaps

 Imp note: the parameter values for vertical metal layer and horizontal metal layer will be 1 more than that specified in the files

# Lab Day 2
 We will now execute floorplan.
 
 command: run_floorplan
 
 ![floorplan](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/e512f240-4843-4e86-8485-ddba74ae7430)
 
After the floorplan run, a .def file will have been created within the results/floorplan directory. We may review floorplan files by checking the floorplan.tcl. The system defaults will have been overriden by switches set in conifg.tcl and further overriden by switches set in sky130A_sky130_fd_sc_hd_config.tcl.

To view the floorplan, Magic is invoked after moving to the results/floorplan directory:

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

![magic floorplan 1](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/d4c53cc3-137c-4b2b-8237-d60a58b7bd13)

One can zoom into Magic layout by selecting an area with left and right mouse click followed by pressing "z" key.


![magic floorplan 2](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/c592ed7f-567d-447e-8fa9-4c6a907ed4b9)
![magic floorplan 3](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/86b6709d-d339-4353-bb38-7e5d479f01c1)
![magic floorplan 4](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/46d54e39-b36c-44b0-a62d-c608805f500a)


## Placement

We will execute the placement step in 2 steps:

Global Placement: Cells will be placed randomly in optimal positions which may not be legal and cells may overlap. Optimization is done through reduction of half parameter wire length. Detailed Placement: It alters the position of cells post global placement so as to legalise them. Legalisation of cells is important from timing point of view.

Optimization is stage where we estimate the lenght and capictance, based on that we add buffers. Ideally, Optimization is done for better timing.

command: magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def

note: use this command in the results/placement directory

![placement 1](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/8d6f512e-a0b4-42ed-a620-b36acd63792b)

![magic placement](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/04ca48d5-4862-496c-b320-08177851f032)

The EDA tool always requires data from the library of gates, which contains all standard cells (and, or, buffer gates,...), macros, IPs, decaps, etc., during all RTL-to-GDSII stages. The library may have distinct flavours for the same cells (various sizes, delays, and threshold voltage). Greater drive strength can drive longer and thicker wires thanks to larger cell sizes. Smaller threshold voltage devices switch more slowly than those with larger threshold voltages (due to larger size).

A single cell needs to go through the cell design flow. The inputs to make a single cell comes from the foundry Process Design Kits:

DRC & LVS Rules = tech files and poly subtrate paramters (CUSTOME LAYOUT COURSE)

SPICE Models = Threshold, linear regions, saturation region equations with added foundry parameters. Including NMOS and PMOS parameteres (Ciruit Deisgn and Spice simulation Course)

User defined Spec = Cell height (separation between power and ground rail), Cell width (depends on drive strength), supply voltage, metal layer requirement (which metal layer the cell needs to work)

The library cell developer must adhere to the rules given on the inputs so that when the cell is used on a real design, there will be no errors. Next is design 

the library cell:

Design the circuit function (Output: circuit design language (CDL))

Model the pmos and nmos that meets input library requirement

Layout the design using Euler's path and sticky diagram to produce best area. This can be done on magic layout tool.The outputs are:

GDSII (layout file)

LEF (defines the width and height of cell)

extract spice netlist .cir (parasitics of each element of cell: resistance, capacitance) Afte design is characterization using GUNA software, where the outputs are timing, noise, and power characterization. .

A typical standard cell characterization flow that is followed in the industry includes the following steps:

a.Read in the models and tech files
b.Read extracted spice Netlist
c.Recognise behavior of the cells
d.Read the subcircuits
e.Attach power sources
f.Apply stimulus to characterization setup
g.Provide neccesary output capacitance loads
h.Provide neccesary simulation commands

All these 8 steps are fed in together as a configuration file to GUNA.

| Timing defintion	 | Value |
| ------------- | ------------- |
| slew_low_rise_thr  | 20% value |
| slew_low_rise_thr | 80% value |
|slew_low_fall_thr	|20% value |
|slew_high_fall_thr |	80% value |
|in_rise_thr	|50% value |
|in_fall_thr	|50% value |
|out_rise_thr	|50% value |
|out_fall_thr	|50% value |

### Propagation Delay 

The time difference between when the transitional input reaches 50% of its final value and when the output reaches 50% of its final value. Poor choice of threshold values lead to negative delay values. Even thought you have taken good threshold values, sometimes depending upon how good or bad the slew, the dealy might be still +ve or -ve.

Propagation delay = time(out_thr) - time(in_thr)

### Transition Time

The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.

Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Low transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)

# Day 3 Design Library Cell using ngspice simulations

## ngspice simulations for CMOS inverter

ngspice is opesoure engine where simulations are done.

### IO Placer revision

PnR is an iterative flow, thus we may alter the environment variables in the fly to see how our design has changed.
Say I want to alter my pin arrangement along the core from being randomly placed at equvi distance to another placement. I would simply set the IO mode variable on the command prompt as shown below.
set ::env(FP_IO_MODE) 2

### SPICE Deck Creation and Simulation for CMOS inverter

We need to establish a SPICE Deck before running a SPICE simulation. The following information is provided by SPICE Deck:

Connectivity of the substrate, Vdd, Vss, and Vin components. The MOS's threshold voltage is adjusted by the substrate.

component values include supply voltage, output load, input gate voltage, and PMOS and NMOS values.

Nodes must be identified and given names in order to define the SPICE Netlist. As an illustration, M1 out in vdd vdd pmos w = 0.375u L = 0.25u,  cload out 0 10f.

simulation instructions

Model file: details of transistor-related parameters CMOS simulation with varying width and length. Regardless of switching, the waveform's shape is essentially the same.

![spice](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/ebcfeeb9-c98a-4726-9523-f1156257b1c4)

The waveform shows that the features hold true for all CMOS sizes. Therefore, CMOS is a reliable circuit and is used in the design of logic gates. 


### Switching Threshold Vm

The Vin = Vout point on the DC Transfer characteristics is the switching threshold of a CMOS inverter.
Since both transistors are currently turned on and in the saturation region, there is a significant likelihood that leakage current, which is current that flows directly from VDD to Ground, will occur.


![2 spice](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/38d70dc0-6465-4de2-8993-94bf7884e4a6)

## Git clone vsdiatdesign

clone the required mag files and spicemodels of inverter,pmos and nmos sky130. The command to clone files from github link is:

git clone https://github.com/nickson-jose/vsdstdcelldesign.git
The information of inverter layout is mentioned in sky130_inv.mag file.
![day 3 git clone](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/aefc2797-10bb-43ce-9f8a-ea6d5ed57ae2)

copy the sky130A.tech file to vsdstdcelldesign by using the command:

cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/

![Screenshot from 2023-06-03 11-38-15](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/c7bb1c67-70b1-4c8d-82f6-5c5d3491d001)

Press "G" to see the blocks

![box inverter](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/925d04e9-83af-4a75-a531-c11cea5dac5f)

## CMOS 16 Mask Fab


1. Selecting a substrate = Layer where the IC is fabricated. Most commonly used is P-type substrate
2. Creating active region for transistor = Separate the transistor regions using SiO2 as isolation

Mask 1 = Covers the photoresist layer that must not be etched away (protects the two transistor active regions)
Photoresist layer = Can be etched away via UV light
Si3N4 layer = Protection layer to prevent SiO2 layer to grow during oxidation (oxidation furnace)
SiO2 layer = Grows during oxidation (LOCOS = Local Oxidation of Silicon) and will act as isolation regions between transistors or active regions

3. N-Well and P-Well Fabrication = Fabricate the substrate needed by PMOS (N-Well) and NMOS (P-Well)

Phosporus (5 valence electron) is used to form N-well
Boron (3 valence electron) is used to form P-Well.
Mask 2 protects the N-Well (PMOS side) while P-Well (NMOS side) is being fabricated then Mask 3 while N-Well (PMOS side) is being fabricated

4. Formation of Gate = Gate fabrication affects threshold voltage. Factors affecting threshold voltage includes:
Main parameters are:
Doping Concentration = Controlled by ion implantation (Mask 4 for Boron implantation in NMOS P-Well and Mask 5 for Arsenic implantation in PMOS N-Well)
Oxide capacitance = Controlled by oxide thickness (SiO2 layer is removed then rebuilt to the desire thickness)
Mask 6 is for gate formation using polysilicon layer.

5. Lightly Doped Drain formation = Before forming the source and drain layer, lightly doped impurity is added:

Mask 7 for N- implantation (lightly doped N-type) for NMOS
Mask 8 for P- implantation (lightly doped P-type) for PMOS.
Heavily doped impurity (N+ for NMOS and P+ for PMOS) is for the actual source and drain but the lightly doped impurity will help maintain spacing between the source and drain and prevent hot electron effect and short channel effect.

6. Source and Drain Formation = Mask 9 is for N+ implantation and Mask 10 for P+ implantation

Channeling is when implantations dig too deep into substrate so add screen oxide before implantation
The side-wall spacers maintains the N-/P- while implanting the N+/P+

7. Form Contacts and Interconnects = TiN is for local interconnections and also for bringing contacts to the top. TiS2 is for the contact to the actual Drain-Gate-Source. Mask 11 is for etching off the TiN interconnect for the first layer contact.

8. Higher Level Metal Formation = We need to planarize first the layer via CMP before adding a metal interconnect. Aluminum contact is used to connect the lower contact to higher metal layer. Process is repeated until the contact reached the outermost layer.

Mask 12 is for first contact hole
Mask 13 is for first Aluminum contact layer
Mask 14 is for second contact hole
Mask 15 is for second Aluminum contact layer.
Mask 16 is for making contact to topmost layer.

## SKY130 basic layer layout and LEF using inverter

We can see the layers needed for the CMOS inverter in Layout. PMOS and NMOS are connected to the inverter.
The NMOS source is connected to ground (here, VGND), the PMOS source is connected to VDD (here, VPWR), and the drains of both PMOS and NMOS are connected to each other and fed to the output (here, Y). The First layer in skywater130 is localinterconnect layer(locali) , above that metal 1 is purple color and metal 2 is pink color. . Place the pointer over the region where you wish to examine links between two distinct components, then press S three times. The connectivity details are provided by the tkson window.


## Design Standard Cell and SPICE extraction in MAGIC

In the Tkson window, we must first specify the bounding box's width and height. Let's assume that the BBOX has a 1.38u width and a 2.72u height. Property Fixed BBOX (0 0 1.32 2.72) is the command to assign these values to magic. 

The layout of the Vdd and GND segments in the metal 1 layer, as well as their corresponding connections, are then determined. We extract the spice and then simulate it in order to understand the logical operation of the inverter. By opening the TKCON window, we may extract it from the spice.

Get the current directory path with pwd. 

Using the command "extract all," a file called sky130_inv.ext has been created.

create spice file using .ext file to be used with our ngspice tool - the commands are
ext2spice cthresh 0 rthresh 0 - extracts parasatic capcitances also since these are actual layers - nothing is created in the folder ext2spice - a file sky130_inv.spice has been created.

## SKY130 Tech file
### Final Spice Deck creation

View the contents of the spice deck. The connections between the pmos and nmos nodes are defined in the spice file subcircuit(subckt)

Sky130_fd_pr_nfet_01v8 for NMOS XO Y A VGND VGND. Cell_name Drain Gate Source Substrate model_name is the correct format. VPWR VPWR sky130_fd_pr_pfet_01v8 for PMOS X1 Y A VPWR VPWR. Cell_name Drain Gate Source Substrate model_name is the correct format.


We would like to define the following connections and additional nodes for these in the spice file for transient analysis.


VGND to VSS

Supply voltage from VPWR to Ground - extra nodes here will be 0 and VDD with a value of 3.3v

sweep in/pulse between A pin and VGND (0) Before, editing the file, make sure scaling is proper, we measure the value of the gride size from the magic layout and define using  .option scale=0.01u in the Deck file.

Now keeping the connection in mind, define the required commands in the file. Along with this we need to include libs for nmos nshort.lib and pmos pshort.lib and define transient analysis commands too. We comment the subckt since we are trying to input the controls and transient analysis also. Model names are changed to nshort_model.0 and pshort_model.0 according to the libs of nmos and pmos.

These voltage sources and simulation commands are defined in the Deck file. VDD VPWR 0 3.3V VSS VGND 0 0V Va A VGND PULSE(0V 3.3V 0 0.1ns 0.1ns 2ns 4ns) .tran 1n 20n .control run .endc .end

![spice new](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/f6ae6372-48d6-46de-ae7a-8263c60fec3d)

![Screenshot 2023-06-03 214734](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/ff4a0a43-52fe-487d-93fa-202566b4d1e3)



### Using ngspice

Spice Deck is done and now to run spice simulation invoke ngspice in the tool and pass the source file.

ngspice sky130_inv.spice

On the prompt you can see the values the ngspice has taken. To see the plot, use

plot y vs time a .

Now we have the transient response, the next objective is to characterise the cell.

![Screenshot from 2023-06-04 08-52-36](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/ee0ddfa5-5385-4515-a10a-de4623c91627)

## CMOS Inverter Standard cell

Four timing parameters determine the inverter standard cell's characterisation.

Time it takes for the production to increase from 20% to 80% of its maximum value. Time it takes for the output to decrease from 80% of the maximum value to 20% of it Cell Rise delay is the interval between a 50% increase in output and a 50% decrease in input. Cell Delay caused by a 50% drop in output compared to a 50% increase in input


You may calculate the aforementioned timing parameters by taking note of various values from the ngspice waveform.

Rise Transition : 2.25421 - 2.18636 = 0.006785 ns / 67.85ps Fall Transitio : 4.09605 - 4.05554 = 0.04051ns/40.51ps Cell Rise Delay : 2.21701 - 2.14989 = 0.06689ns/66.89ps  Cell Fall Delay : 4.07816 - 4.05011 = 0.02805ns/28.05ps

## LAB 
### MAGIC and Skywater's DRC

refer to "http://opencircuitdesign.com/magic.com" to get knowledge about Magic.

Sky130 pdk URL: "https://skywater-pdk.readthedocs.io/en/main/"

### Sky130s pdk intro and Steps to download labs

setup to view the layouts

1)For extracting and generating views, Google/skywater repo files were built with Magic

2)Technology file dependency is more for any layout. hence, this file is created first.

3)Since, Pdk is still under development, there are some unfinished tech files and these are packaged for magic along with lab exercise layout and bunch of stuff into the tar ball

We can download the packaged files from web using the following command in your terminal. 

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

![Screenshot 2023-06-04 012005](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/fa1514be-b209-4e5a-b7f9-a70bd3133d3e)


then use:  tar - tap archiver create and extract a tar archive file.

to extract tar file:  tar -xfz drc_tests.tgz

![Screenshot 2023-06-04 012111](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/63b421f7-c448-452e-809b-8162cc3e66b4)


Now run MAGIC

For better graphics use command magic -d XR 

Now, lets see an example of simple failing set of rules of metal 3 layer. you can either run this by magic command line magic -d XR metal3.mag or from the magic console window, menu - file - open -load file9here, metal3.mag)

![after tar image](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/23f1e72d-b758-44eb-90c6-04e728310ab3)

We have few drc errors and calls out a rule number. You can see these rules on google skywater pdk read the doc page. From metal 3.4 drc rules, Via2 must be enclosed by metal3 by atleast 0.065u. Magic tablet is of using many derived layers and in which via is one. Via represents the area filled with contact cuts. Draw a large area of M3 contatc using mouse pointer hovering over the m3contact icon on the side toolbar. Now with cursor box around the m3 area, type command cif see VIA2 . This create contatc cuts which are bloack sqaure shaped. These dont exist on the drawn layout, but they represent as mask layer VIA2, that will end up in the GDS Futher details about these are metioned in cif output section in tech file. The view we see is feedback entry and can dismiss it with feed clear We use snap internal command snap int for the cursor to move along the edge of the grid. There are few spacing rukes metioned like spacing between Via2 and metal 3 is 0.065u. If we put the curosor between the contact cut and drawn via edge and click box in tkcon command, we will get the distance. The tool automatically places and do spacing of the contact, there wont be any DRC errors and the distance will not be smaller than the specified one.

![Screenshot 2023-06-04 014705](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/730a7db3-8f64-41a4-8511-e95668a585eb)

### Load Sky130 tech rules for drc challenges

First load the poly file by load poly.mag on tkcon window.

Finding the error by mouse cursor and find the box area, Poly.9 is violated due to spacing between polyres and poly

![Screenshot 2023-06-04 020707](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/dc914568-7890-4216-b6a3-2f217ac6c896)

Now, poly.9 is spacing between polyres to poly and poly to diff/tap. Once we resolve the polyres to poly, poly to tap / diff got violations by providing spacing for tap/diff. in tech,

Again load the tech file, check drc and the issue will be solved

# Day 4 Pre-layout Timing analysis and CTS

## Timing Analysis and Clock Tree Synthesis (CTS)

### Standard Cell LEF generation

The whole mag information is not required for placement. All that is necessary are the cell's PR border, I/O ports, power rails, and ground rails. In the LEF file, this information is defined. The primary goal is to take lef out of the mag file and plug it into our design process.

### Grid into Track info

Track: A line or path on which metal layer routing is drawn. The standard cell's height is specified by the track.

A few rules must be fulfilled in order to implement our own stdcell.

I/O ports must be located at the point where horizontal and vertical rails converge.
Standard cell width and height are odd multiples of vertical track pitch and horizontal track pitch.

li1 X 0.23 0.46 
li1 Y 0.17 0.34

![tracks info](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/33ba8b38-6b07-4b2f-872c-f04336a89514)

This information is defined in tracks.info. The syntax is metal_layer direction offset spacing

Create Port Definition:

certain properties and definitions need to be set to the pins of the cell. For LEF files, a cell that contains ports is written as a macro cell, and the ports are the declared as PINs of the macro.

The way to define a port is through Magic console and following are the steps:

In Magic Layout window, first source the .mag file for the design (here inverter). Then Edit >> Text which opens up a dialogue box.
When you double press S at the I/O lables, the text automatically takes the string name and size. Ensure the Port enable checkbox is checked and default checkbox is unchecked

After defining ports, the next step is setting port class and port use attributes.

####Setting port class:

Select port A in magic:

port class input
port use signal
Select Y area

port class output
port class signal
Select VPWR area

port class inout
port use power
Select VGND area

port class inout
port use ground


### Custom cell naming and lef extraction

Name the custom cell through tkcon window as sky130_vsdinv.mag. This gets created in openlane/vsdstdcelldesign directory

use "lef.write" to carry out lef extraction

![lef write](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/89eba7ad-cf97-4bc2-b335-73be4982c6ae)

### Integrating custom cell in OpenLANE
In order to include our custom standard cell to ur design and run the first step synthesis, copy the sky130_vsdinv.lef file to the designs/picorv32a/src directory. Since abc maps the standard cell to a library, there must be a library that defines the CMOS inverter. The sky130_fd_sc_hd_typical.lib as well as fast and slow libs files from vsdstdcelldesign/libs directory needs to be copied to the designs/picorv32a/src directory. If you are interested to check our cell in lib and lef, go to lib and lef folders

Next, modifiy the config.tcl by adding few extra definitions like abc synthesis mapping to typical.lib, other three are used for sta analysis and to include extra lefs(our design lef) to flow

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130/sky130_fd_sc_hd__typical.lib"
set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

Change the default of "SYNTH_STRATEGY" from "AREA 0" to "DELAY 0" in configuration/synthesis.tcl

In order to integrate the standard cell in the OpenLANE flow, invoke openLANE as usual and carry out following steps:

prep -design picorv32a -tag 03-06-08-35 -overwrite 
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis

after synthesis, my timing is clean.

![customised cell in synthesis](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/f5fed763-cf8b-4734-868f-2b5aa4af052e)


![slack successful](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/95a58484-dcca-4a73-b94d-24b89598becb)


now run the following commands:
init_floorplan
place_io
global_placement_or
tap_decap_or
(since run_floorplan was giving error)

![detailed placement](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/1852fc90-47cb-4f1f-9a8e-f32a2e9557df)

To check the layout invoke magic from the results/placement directory:

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

![Screenshot 2023-06-05 143250](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/1d8a7682-42e0-408a-b6a5-e7569ca7b514)

Take the cursor to the cell and press "S". then write "expand" in tkcon.

![Screenshot 2023-06-05 212545](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/88d95f60-b9b9-447a-b85c-ac80b2607b7d)

### Post-synthesis timing analysis Using OpenSTA
Create 2 files. my_base.sdc and pre_sta.conf

my_base.sdc:

![my_base](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/6961098f-d250-47e8-be4a-90682d756523)

pre_sta:

![presta](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/ea5619e7-72af-4153-9afe-fb50333779c8)

Now type "sta pre_sta.conf"

Since I had no violations, I skipped this step.

The PLL, which contains an internal circuit with cells and some logic, generates the clock. Depending on the ckt, there could be changes in the clock generation. Collectively, these fluctuations are referred to as clock uncertainty. Jitter is one of the parameters in that. It is unlikely that the clock will arrive at that precise moment without any adjustments. Because of this, it is known as clock_uncertainty. Margin, Skew, and Jitter enter clock_uncertainty.

 Clock jitter is the movement of the edge away from its initial location.


According to the timing report, we can increase slack by replacing the cells with larger ones that have a higher drive strength, and we will notice a noticeable difference in the slack.

## Clock Tree Synthesis using Tritoncts

In this stage clock is propagated and make sure that clock reaches each and every clock pin from clock source with mininimum skew and insertion delay. Inorder to do this, we implement H-tree using mid point strategy. For balancing the skews, we use clock invteres or bufferes in the clock path. Before attempting to run CTS in TritonCTS tool, if the slack was attempted to be reduced in previous run, the netlist may have gotten modified by cell replacement techniques. Therefore, the verilog file needs to be modified using the write_verilog command. Then, the synthesis, floorplan and placement is run again. To run CTS use the below command:

run_cts

After CTS run, my slack values are

setup : 4.76 , Hold : 0.3945

Since, clock is propagated, from this stage, we do timing analysis with real clocks. From now post cts analysis is performed by operoad within the openlane flow
openroad
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/03-07_11-25/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock (all_clocks)
report_checks -path_delay min_max -format full_clock_expanded -digits 4

After performing Timing analysis, my slack values are

 Setup : 4.0565 , Hold : -0.1673

Use these commands if there are violations and change their values:
echo $::env(CTS_CLK_BUFFER_LIST)
set $::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
echo $::env(CTS_CLK_BUFFER_LIST)

# Day 5
## Final steps in RTL2GDS
### Maze Routing and Lee's algorithm

A physical connection between two pins is called routing. The algorithm uses the pins as its source and target, and it determines the optimum route between them if a connection can be made between them.

The Maze Routing algorithm is one such technique, and the Lee algorithm is one potential remedy for Maze routing issues.

Earlier, when customising the cell, we established a grid. Similar to how a floorplan generates a grid for routing. Using a routing grid, the Lee algorithm establishes the source and target locations and then seeks the shortest/best route between them.

From 1 until it reaches the target (let's say 7, for example), it makes labels for the nearby grids around the source. There will be numerous routes from 1 to 7, including zigzag and L-shaped routes. Lee Alogirthm favours the best path, which is L-shaped and does not zigzag. It must follow the zigzag course if there are no L-shaped routes. The global routing is done using this.

There are restrictions on it. It first generates the maze before beginning to number the moves from the source to the target. While routing with just two pins is simple, doing it with millions of pins takes a lot of time. There are more analogies that operate in a similar way.



### Design rule check(DRC)


DRC verifies whether a design meets the predefined process technology rules given by the foundry for its manufacturing. DRC checking is an essential part of the physical design flow and ensures the design meets manufacturing requirements and will not result in a chip failure. It defines the Quality of chip. They are so many DRCs, let us see few of them

Design rules for physical wires

Minimum width of the wire
Minimum spacing between the wires
Minimum pitch of the wire To solve signal short violation, we take the metal layer and put it on to upper metal layer. we check via rules
Via width
via spacing

## Power Distribution Network generation
Run "gen_pdn" in OpenLANE 
we can check whether PDN has been created or no by check the current def environment variable:  echo S::env(CURRENT_DEF).

Once the command is given, power distribution netwrok is generated.
The power distribution network has to take the design_cts.def as the input def file.
Power rings,strapes and rails are created by PDN.
From VDD and VSS pads, power is drawn to power rings.
Next, the horizontal and vertical strapes connected to rings draw the power from strapes.
Stapes are connected to rings and these rings are connected to std cells. So, standard cells get power from rails.
The standard cells are designed such that it's height is multiples of the vertical tracks /track pitch. Here, the pitch is 2.72. Only if the above conditions are adhered it is possible to power the standard cells.
There are definitions for the straps and the rails. In this design, straps are at metal layer 4 and 5 and the standard cell rails are at the metal layer 1. Vias connect accross the layers as required.
![pdn_gen](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/f17bbd17-f4c2-4264-805c-79a7cb5298b9)


## Routing
Basically, the entire routing procedure is quite hard in all routing EDA tools, including OpenLANE and Commercial EDA tools, due to the vast amount of space. Global routing and detailed routing were the two steps they separated the routing process into.

Two different engine types carry out two steps of routing:


Global routing is a type of 3D routing graph that divides the routing region into rectangular grid cells. FASTE ROUTE is the engine that does global routing.

Detailed routing - Finer grids and routing guides used to implement physical wiring TritonRoute Fast Route generates the routing guides, whereas TritonRoute uses the Global Route and then completes the routing with a few strategies and optimisations to find the best route connect the pins.




## Features of TritonRoute
Performs Initial detail route
Honouring pre-processed route guides - attempts to route within the route guides
      Initial route guide - see the directions of the prefered route guides. If any non direction routing guides are found it divides it into unit widths.
      Splitting - It splits non direction routing guides into unit widths
      Merging - guides that are orthogonal(touching guides) to to the prefered guides are merged.
      Bridging - gudies that are parallel to the perfered routing guides are bridged with an additional layer
      preprocessed guides
      Works on MILP(Mixed Integer linear programming) based panel routing scheme with Intra-layer parallel and Inter-layer sequential routing framework
Now use "run_routing" in OpenLANE

![routing ](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/cc2126f4-ef39-4304-8e75-9b02618b3b77)
    
 To see the design:
    
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.routing.def &

   ![rout](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/1d2e5933-89ad-4147-b832-fc4f29b2c8b1)
![final](https://github.com/Jainil25/VSDIAT-Physical_Design-workshop/assets/105313126/67139965-5eb9-4148-b222-475ec66c9fad)


 
 

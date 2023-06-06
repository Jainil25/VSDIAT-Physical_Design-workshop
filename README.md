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
| slew_low_rise_thr  | 20%  |
| slew_low_rise_thr | 80% |
|slew_low_fall_thr	|20% value |
|slew_high_fall_thr |	80% value |
|in_rise_thr	|50% value |
|in_fall_thr	|50% value |
|out_rise_thr	|50% value |
|out_fall_thr	|50% value |






 
 

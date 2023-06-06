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

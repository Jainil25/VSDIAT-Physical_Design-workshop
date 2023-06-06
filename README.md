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





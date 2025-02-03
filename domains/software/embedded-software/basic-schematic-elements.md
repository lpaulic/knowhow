# Basic schematic elements

Hardwre department in Bytelab uses [Altium Designer](https://www.altium.com/altium-designer). The nomenclature
depends on the hardware design tool used but the differences are not big.

Basic elements in the schematis are:
- Net labels
    - Schematic design tools label each net (piece of wire on the schematic) a certain name (based on the components it interconnects).
    Adding a net label names the net as the user wants so the automatically generate one is not used. If the same net label is applied
    to two separate pieces of wire, in Altium, they will be handled as one wire (short circuited).
- Ports
    - Schematic diagram, when complex, is devidied in multiple schematic sheets. If one signal needs to go from one sheet to another,
    ports need to be used. In order for the ports to be recognized as connected (from two separated sheets), they must me named the same.
    Convention is to have the port name the same as the net label
- Crossed components
    - marked as DNP, see [abbreviations](400.1-hardware-for-fw-devs.md)
- Component designator
    - Unique component name in the design, comprised of a prefix (R, L, C, etc.) and a suffix (number starting from 1)
    - The convention is: R9 for resistors, C2 for capacitors, L6 for inductors, T4 for transistors, D3 for diodes, U1 for ICs, etc.
- Component manufacturer Part Number
    - Parameter required to be in the schematics PDF output
    - Required for all but the generic ones (e.g. resistor, capacitor, ...)
- Comment
    - Component's parameter is written
- Design note
- DVT note
- Software config note

FW engineers do not have to use the Altium, they view/review the schemas through PDFs


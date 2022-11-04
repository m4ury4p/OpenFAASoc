# OpenFAASoc flow
Repository containing my part in openfaasoc project flow


## Overview to FAASoc flow:
The FASoC Program is focused on developing a complete system-on-chip (SoC) synthesis tool from user specification to GDSII. FASoC leverages a differentiating technology to automatically synthesize “correct-by-construction” Verilog descriptions for both analog and digital circuits and enable a portable, single pass implementation flow. The SoC synthesis tool realizes analog circuits, including PLLs, power management, ADCs, and sensor interfaces by recasting them as structures composed largely of digital components while maintaining analog performance. They are then expressed as synthesizable Verilog blocks composed of digital standard cells augmented with a few auxiliary cells generated with an automatic cell generation tool. By expanding the IPXACT format and the Socrates tool from ARM, we then enable composition of vast numbers of digital and analog components into a single correct-by-construction design. 


## Tools for installation:
<h4> Tool installation steps can be found here: </h4>

https://openfasoc.readthedocs.io/en/latest/getting-started.html#installation

You can either follow the express installation or the manual installation steps.

The following tools will be required for complete flow
1. OpenRoad
2. Magic
3. Yosys
4. Klayout
5. Open_PDK
6. Netgen

## Understanding the floorplan flow:
  The flow after synthesis ot floorplan is given here.
<b>input</b> : Verilog netlist files which contain the description of the circuit.
<b>output</b> : 2_1floorplan.odb , floorplan_io.odb, floorplan.macro.odb, 3_place.sdc

## BLock diagram:



## Detailed explanation:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_45.png)
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_46.png)

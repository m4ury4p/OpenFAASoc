# OpenFAASoc flow
Repository containing my part in openfaasoc project flow


## Overview to FAASoc flow:
The FASoC Program is focused on developing a complete system-on-chip (SoC) synthesis tool from user specification to GDSII. FASoC leverages a differentiating technology to automatically synthesize “correct-by-construction” Verilog descriptions for both analog and digital circuits and enable a portable, single pass implementation flow. The SoC synthesis tool realizes analog circuits, including PLLs, power management, ADCs, and sensor interfaces by recasting them as structures composed largely of digital components while maintaining analog performance. They are then expressed as synthesizable Verilog blocks composed of digital standard cells augmented with a few auxiliary cells generated with an automatic cell generation tool. By expanding the IPXACT format and the Socrates tool from ARM, we then enable composition of vast numbers of digital and analog components into a single correct-by-construction design. 


# Tools for installation:
<h4> Tool installation steps can be found here: </h4>

https://openfasoc.readthedocs.io/en/latest/getting-started.html#installation

You can either follow the express installation or the manual installation steps.

## The following tools will be required for complete flow

### 1. OpenROAD

https://github.com/The-OpenROAD-Project/OpenROAD
<br>
### 2. Magic
https://github.com/RTimothyEdwards/magic
<br>
### 3. Yosys
https://github.com/The-OpenROAD-Project/yosys
<br>
### 4. Klayout
https://github.com/KLayout/klayout
<br>
### 5. Open_PDK

https://github.com/RTimothyEdwards/open_pdks
<br>
### 6. Netgen

https://github.com/RTimothyEdwards/netgen
<br>

## Understanding the floorplan flow:

after running the command ```make sky130hd_temp_verilog```, the python file ``` openfasoc/generators/temp-sense-gen/tools/temp-sense-gen.py ``` is executed.<br>

This step converts template verilog files,synthesis.odb and auxilary cells into netlist verilog files.<br>

These new netlist files are now available in the ```OpenFASOC/openfasoc/generators/temp-sense-gen/src folder``` and the ```OpenFASOC/openfasoc/generators/temp-sense-gen/flow/design/src/tempsense ``` <br>

The netlist file:<br>
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/netlist_of.png)

The placement check happens here:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/placement_flow.png)

## BLock diagram:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/total_flow.png)


## Detailed explanation:

The project directory in flow contains the python script to access the 

![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_45.png)
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_46.png)

## Results:
  After running the flow, the results directory will be generated. It will look like this:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/ss_folder.png)

  The flow after synthesis ot floorplan is given here.
<b>input</b> : Verilog netlist files which contain the description of the circuit like TEMP_analog_hv_nl.v and TEMP_analog_lv_nl.v,1_synthesis.odb.
<b>output</b> : 2_1floorplan.odb , floorplan_io.odb, floorplan.macro.odb.

Currently trying to figure out how to convert.odb files into .def files which can be viewed using klayout or magic tools.

<h4> Running the OpenFASOC Flow for temperature sensor generator </h4>

1. Clone the openfasoc git repo using the below command

```
git clone https://github.com/idea-fasoc/openfasoc
```

2. Move to the required temp-sense-gen directory 
```
cd openfasoc/generators/temp-sense-gen
```

3. Give the following commands

```
make
```

## Author 

- **Maurya Patel** 


## Contributors 

- **Maurya Patel** 
- **Kunal Ghosh** 


## Acknowledgments

- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.

## Contact Information

- Maurya Patel, Integrated MTech Student, International Institute of Information Technology, Bangalore  Maurya.Patel@iiitb.ac.in
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com



# OpenFASOC flow
Repository containing my part in openfaasoc project flow


## Overview to FASOC flow:
The FASOC Program is focused on developing a complete system-on-chip (SoC) synthesis tool from user specification to GDSII. FASoC leverages a differentiating technology to automatically synthesize “correct-by-construction” Verilog descriptions for both analog and digital circuits and enable a portable, single pass implementation flow. The SoC synthesis tool realizes analog circuits, including PLLs, power management, ADCs, and sensor interfaces by recasting them as structures composed largely of digital components while maintaining analog performance. They are then expressed as synthesizable Verilog blocks composed of digital standard cells augmented with a few auxiliary cells generated with an automatic cell generation tool. By expanding the IPXACT format and the Socrates tool from ARM, we then enable composition of vast numbers of digital and analog components into a single correct-by-construction design. 



This is an example of auxiliary cell:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/header_cell.png)
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/SLC.png)




## Block diagram:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/total_flow.png)





# Installation
## OpenFASOC:
The command used to install OpenFASOC are 
```
git clone https://github.com/idea-fasoc/openfasoc
cd openfasoc
pip install -r requirements.txt
```
For the complete steps of installing OpenFASOC, refer Manual Installation from [here](https://github.com/idea-fasoc/OpenFASOC/blob/main/docs/source/getting-started.rst). 

## OpenROAD: 
OpenROAD is an integrated chip physical design tool that takes a design from synthesized Verilog to routed layout. OpenROAD uses the OpenDB database and OpenSTA for static timing analysis. Documentation is also available [here](https://openroad.readthedocs.io/en/latest/main/README.html).


The commands to install OpenROAD are,
```
git clone --recursive https://github.com/The-OpenROAD-Project/OpenROAD.git
cd OpenROAD
./etc/DependencyInstaller.sh
./etc/DependencyInstaller.sh -run
./etc/DependencyInstaller.sh -dev
mkdir build
cd build
cmake ..
make
```

## Klayout
To download Klayout, we need to install the following dependencies: qt5-default, qttools5-dev, libqt5xmlpatterns5-dev, qtmultimedia5-dev, libqt5multimediawidgets5 and libqt5svg5-dev.

```
sudo apt-get install -y libqt5widgets5
sudo dpkg -i klayout_0.27.11-1_amd64.deb
```

## Netgen
To install Netgen use the following commands, 
```
sudo add-apt-repository ppa:ngsolve/ngsolve
sudo apt-get update
sudo apt-get install ngsolve
```

## Yosys
Yosys is a framework for Verilog RTL synthesis. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains. Yosys can be adapted to perform any synthesis job by combining the existing passes (algorithms) using synthesis scripts and adding additional passes as needed by extending the Yosys C++ code base.


The following commands will install yosys
 ```
 sudo apt-get install build-essential clang bison flex \
	libreadline-dev gawk tcl-dev libffi-dev git \
	graphviz xdot pkg-config python3 libboost-system-dev \
	libboost-python-dev libboost-filesystem-dev zlib1g-dev
```

## Magic
Run following commands one by one to fulfill the system requirement.
#### Prerequisites for magic
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
```

# Tools for installation:
<h4> Tool installation steps can be found here: </h4>

https://openfasoc.readthedocs.io/en/latest/getting-started.html#installation

You can either follow the express installation or the manual installation steps.

## These are the github links for tools in case they aren't available as package repositories:
The steps to install the tools are given in the respective makefiles(or install files if present) of their respective github repositories.
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


# Detailed explanation:

In our part, we take the synth.v file and synth.sdc files as input and run the floorplan.tcl script. The reports of the whole process will be stored into floorplan.log files.

The project directory in flow contains the python script to access the 

![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_45.png)
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/Screenshot_46.png)

## Results:
  After running the flow, the results directory will be generated. It will look like this:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/ss_folder.png)


The die area is as shown below:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/floorplan_stats.png)

The final output is shown below:
![image](https://github.com/m4ury4p/OpenFAASoc_flow/blob/main/final.png)

  The flow after synthesis ot floorplan is given here.
<b>input</b> : Verilog netlist files which contain the description of the circuit like TEMP_analog_hv_nl.v and TEMP_analog_lv_nl.v,1_synthesis.odb.
<b>output</b> : 2_1floorplan.odb , floorplan_io.odb, floorplan.macro.odb adn 2_floorplan.sdc files.


The floorplan.odb and floorplan.sdc files will be passed to our next stage, which is placement in our case.<br>
Then the remaining steps will take place and our flow will be complete.


# Future plans:

Trying to learn more about the .odb files and how this flow can be further optimized. Also trying to make some improvements with the OpenROAD tool.

# Errors encountered:

- lemon version problem

# Note:
There were some issues in running the flow in my system. The whole flow can be viewed in the given github repo:<br>
https://github.com/TejasBN28/OpenFASOC#4-PLL-Generator


## Author 

- **Maurya Patel** 


## Contributors 

- **Maurya Patel**


## Acknowledgments

- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd.
- Tejas BN, MTech Student, IIIT Bangalore

## Contact Information

- Maurya Patel, Integrated MTech Student, International Institute of Information Technology, Bangalore  Maurya.Patel@iiitb.ac.in
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com



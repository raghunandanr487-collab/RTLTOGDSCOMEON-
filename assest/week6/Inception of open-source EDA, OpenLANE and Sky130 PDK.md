## 📦pakage 

- In any embedded board, the component we commonly refer to as “the chip” is actually just the package. The package is a protective enclosure surrounding the real silicon die. The actual manufactured chip (the silicon die) sits at the center of this package, and all external pins are connected to the die through a process called wire bonding, where very fine metal wires form the electrical connections between the die and the package leads.

<img width="473" height="361" alt="image" src="https://github.com/user-attachments/assets/d264af04-ee4b-4e40-8975-876b002a75bc" />


## 🍪 now we will see the chip 


<img width="490" height="313" alt="image" src="https://github.com/user-attachments/assets/bd32d12a-7118-4844-a533-6eb403125e7a" />


## 🎲 Die

- The die is the actual silicon chip manufactured in the semiconductor fabrication process.
It contains all the transistors, logic gates, memories, analog circuits, and interconnects that implement the functionality of the IC.

- The die is extremely small and sits at the center of the package.

## 🔑 pads

- Pads are the metal contact points placed around the edges of the die.
Their purpose is to:

- Provide connection between the internal circuitry and the outside world

- Serve as bonding points for wire bonding or flip-chip bumps

- Handle power (VDD, VSS), I/O signals, reset, clock, etc.

- Pads are designed with ESD protection, output drivers, and input buffers to safely interface with external signals.

- Each pad is connected to a pin on the chip package.

## ⏭️Core

- The core is the main functional area of the chip—it contains:

- Logic circuits (combinational + sequential)

- Memory blocks

- Processing units

- Peripherals

- Routing and power distribution lines

- The core interacts with the outside world only through the pads.
  Internal signals never directly reach package pins. They must go through a pad cell.

ISA (Intruction Set Architecture)
- A C program which has to be run on a specific hardware layout which is the interior of a chip    in your laptop, there is certain flow to be followed.
- Initially, this particular C program is compiled in it's assembly language program which is  nothing but RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture).
- Following this, the assembly language program is then converted to machine language program - which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
- Directly after this, we've to implement this RISC-V specification using some RTL (a Hardware Description Language). Finally, from the RTL to Layout it is a standard PnR or RTL to GDSII flow.


<img width="437" height="286" alt="image" src="https://github.com/user-attachments/assets/c0fbb604-4989-4358-b6dc-084fb999db61" />

- Application enters the system software layer, which is responsible for translating high-level programs into binary code.
- System software is made up of multiple components, with the key ones being:

 - Operating System (OS)

- Compiler

- Assembler

- The OS provides system-level functions written in high-level languages such as C, C++, Java, or VB.

- The compiler takes the high-level code and converts it into hardware-specific instructions.
The syntax and instruction format depend on the CPU architecture.

- The assembler then processes these instructions and translates them into binary machine code (0s and 1s).

- This binary machine code is finally loaded into the hardware, where the processor interprets the bit patterns and executes the required operations.


<img width="1833" height="1162" alt="Screenshot 2025-10-26 170300" src="https://github.com/user-attachments/assets/3a2841a6-6ef0-4c66-a0aa-3eb27380e482" />

## 🔮 Explanation of the Diagram

- This image shows the complete flow of converting software instructions into actual hardware      behavior inside a processor.

- High-level instructions (like add x6, x10, x6) are first written in assembly language.

- These instructions pass through the Assembler, which converts them into binary machine code (sequence of 0s and 1s).
This conversion follows the Instruction Set Architecture (ISA) of the processor.

- The binary machine code is then provided to the RTL hardware design (written in Verilog).
This RTL describes how the CPU decodes instructions and performs the operations.

- The RTL is then synthesized to generate a gate-level netlist, which shows how basic logic gates implement the instruction behavior.

- The synthesized netlist is sent through physical design, where actual layout (placement and routing) is created.
This layout represents the real silicon hardware where transistors, wires, power rails, and logic cells are placed.

- Finally, this physical layout becomes the chip hardware, capable of executing the same instructions that started as high-level assembly code.



<img width="1835" height="1029" alt="Screenshot 2025-10-26 172027" src="https://github.com/user-attachments/assets/eb3ab6a4-3bbb-45af-ad27-4198be7764ed" />


### ⚓ EDA Tools
- Tools like Qflow, OpenROAD, and OpenLANE are used to automate the ASIC design flow, including synthesis, placement, routing, and physical verification.

### RTL Designs
- These are the hardware descriptions written in Verilog or VHDL.

### PDK Data
- The Process Design Kit (PDK) provides all the manufacturing rules, device models, and design     constraints required to build the chip.
-  The image refers to the Google–SkyWater 130nm Open Source PDK, available on GitHub.



<img width="1845" height="1006" alt="Screenshot 2025-10-26 172446" src="https://github.com/user-attachments/assets/510bd0f2-b55f-4cd7-8ac9-e07c08cd2333" />

- This slide shows the ASIC physical design flow, beginning from RTL and ending at the final GDSII layout.

 ### RTL (Verilog/VHDL)
- The design starts with RTL code describing hardware behavior.

### Synthesis
- RTL is converted into a gate-level circuit using cells from the Standard Cell Library (SCL).
Example: an always block using if/else becomes a set of logic gates and flip-flops.

### Floorplanning + Power Planning (FP + PP)
- Defines the chip’s outline, placement of blocks, and power grid structure.

### Placement
- Standard cells from synthesis are placed at specific physical locations on the chip.

### Clock Tree Synthesis (CTS)
- The clock network is built to ensure the clock reaches all flip-flops with minimal skew.

### Routing
- All placed cells are wired together using metal layers according to PDK rules.

### Sign-Off
- Final verification steps (DRC, LVS, STA) ensure the design is correct and meets timing.

### GDSII Output
- The final layout is exported as a GDSII file, which is the format used for chip fabrication.



<img width="1217" height="434" alt="Screenshot 2025-10-26 172502" src="https://github.com/user-attachments/assets/441628c0-8d5c-43cf-bc98-d1240b38184f" />


- Standard cells are pre-designed logic blocks (such as INV, NAND2, XOR2) that follow a regular   and uniform layout structure. This regularity ensures consistent height, aligned power rails,   and predictable routing channels, making automatic placement and routing much easier during     ASIC design.




<img width="1202" height="433" alt="Screenshot 2025-10-26 172711" src="https://github.com/user-attachments/assets/143ed0f4-9991-4853-827b-647a14e0076e" />


- Chip floor-planning involves dividing the chip die into dedicated regions for major             functional blocks—such as the CPU, SRAM, Flash controller, and I/O units—and arranging the      I/O pads around the perimeter. A good floorplan ensures efficient data flow, short              interconnects, and proper placement of power, memory, and logic blocks on the chip.




<img width="1061" height="415" alt="Screenshot 2025-10-26 172720" src="https://github.com/user-attachments/assets/b6101266-41e4-4d3a-a1d8-64c816815b49" />

- Macro floor-planning defines the overall chip dimensions, arranges the I/O pin locations around the border, and sets up the internal placement rows where standard cells will be placed. This step forms the structural foundation for the entire physical design.


<img width="962" height="430" alt="Screenshot 2025-10-26 172731" src="https://github.com/user-attachments/assets/d528e794-d558-4ac5-972f-928e655f8d3a" />



- Power planning ensures that the entire chip receives stable power (VDD) and ground (VSS). Power pads bring power onto the chip, power rings distribute it around the perimeter, and power straps carry it across the core area. Together, they create a robust power delivery network that supplies all standard cells and blocks inside the chip.



<img width="1202" height="442" alt="Screenshot 2025-10-26 173300" src="https://github.com/user-attachments/assets/77ed759a-40cf-408e-a5e9-a84d559e4ab2" />


- A clock distribution network is designed to deliver the clock signal uniformly to all sequential elements in the chip, such as flip-flops. The goal is to minimize clock skew and ensure that the clock reaches every part of the chip in a balanced way. This network is typically built in structured shapes—like H-trees or X-trees—to maintain symmetry and achieve consistent timing.


### THESE  ARE SOME SCREENSHOTS
<img width="684" height="384" alt="Screenshot 2025-10-26 173507" src="https://github.com/user-attachments/assets/ce5ea1a4-b74a-4260-bcad-fc412f200596" />




<img width="1744" height="1008" alt="Screenshot 2025-10-26 175418" src="https://github.com/user-attachments/assets/68a66c58-23c4-467d-8e0a-92c80edd73c2" />

### Explanation

- Antenna rule violations occur when long metal interconnects accumulate charge during fabrication, potentially damaging the gate oxide of a transistor. To fix this, one solution is bridging, where the router connects part of the long wire to a higher metal layer so that the wire is broken into shorter segments. This reduces the effective antenna area and prevents excessive charge buildup, though it requires router awareness to implement correctly.



<img width="1665" height="928" alt="Screenshot 2025-10-26 175432" src="https://github.com/user-attachments/assets/40284e51-dc40-4bdb-bf0f-d1835a1e64ab" />



<img width="1702" height="920" alt="Screenshot 2025-10-26 175510" src="https://github.com/user-attachments/assets/dfee9183-e7d6-4141-b656-faef15baf697" />



<img width="1082" height="842" alt="Screenshot 2025-10-26 175528" src="https://github.com/user-attachments/assets/1c5cc09b-cbcf-4cfa-a8f9-a016e067e512" />



## routing 

<img width="1036" height="567" alt="image" src="https://github.com/user-attachments/assets/d70eb96c-9052-4f06-aff8-bd19cdd2e82d" />

- skywater PDK has 6 routing layers in which the lowest layer is called the local interconnect layer which is a Titanium Nitride layer the following 5 layers are all Aluminium layers.

- Once done with the routing the final layout can be generated which undergoes various Sign-Off checks.
- Design Rules Checking (DRC) which verifies that the final layout honours all design fabrication rules.
- Layout Vs Schematic (LVS) which verifies that the final layout functionality matches the gate-level netlist that we started with.
- Static Timing Analysis (STA) to verify that the design runs at the designated clock frequency.







<img width="1027" height="543" alt="image" src="https://github.com/user-attachments/assets/8950abb4-3691-4d9e-b8fc-32cca85906f1" />


## ❤️‍🩹Implementation

### Section 1 Tasks

- Run the OpenLANE flow for the picorv32a design to perform synthesis and generate all required output files.

- Compute the flip-flop ratio using the formula:

     Flop Ratio = Number of D Flip Flops / Total Number of Cells

     Percentage of DFFs = Flop Ratio × 100

### this the file which we use 


<img width="716" height="553" alt="Screenshot 2025-10-27 204850" src="https://github.com/user-attachments/assets/5b4a6ed5-da7c-4f5a-b9e5-b86e690174d4" />


<img width="722" height="562" alt="Screenshot 2025-10-29 022332" src="https://github.com/user-attachments/assets/435ac923-7a34-4eda-9b06-30fcacf5a3c6" />


<img width="728" height="547" alt="Screenshot 2025-10-29 022513" src="https://github.com/user-attachments/assets/d495f23e-8f32-4f81-ba56-8e3a2abf6472" />


### now we wills ee the commands which is used here 

```bash
 
sudo docker run -it --rm \
-v /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane:/openLANE_flow \
-v /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks:/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks \
-e PDK_ROOT=/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks \
-u $(id -u vsduser):$(id -g vsduser) \
efabless/openlane:v0.15 \
```


```bash
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```



<img width="723" height="454" alt="Screenshot 2025-10-31 170542" src="https://github.com/user-attachments/assets/a9610705-7a3d-474a-9628-3cc7c7d7226c" />

### after running the synthasis 

<img width="897" height="1016" alt="Screenshot 2025-10-29 195807" src="https://github.com/user-attachments/assets/97ce6d0e-edc3-4dec-9871-60fce77a1471" />




### on calculating thde flop ratio 


- Flop Ratio = 1613 / 14876 = 0.108429685

- Percentage of DFFs = 0.108429685 × 100 = 10.84296854 %


























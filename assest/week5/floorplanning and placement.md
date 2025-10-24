
# 💪floorplanning 

## Definition: Floorplanning is the process of allocating space, determining the shape and size of the chip, and defining the precise locations of the major functional blocks (macros, I/O pads, etc.) before the standard cells (logic gates) are placed.

### 🌆there are different areas in the floorplaning

- Die Area: The total physical area of the silicon chip.
- Core Area: The inner region where all the logic (standard cells and macros) is actually placed. Its size is determined by the required Core Utilization (usually 70%-85%), which is the ratio of standard cell area to the available core area.

### 📍 I/O Pad / Pin Placement:
- I/O (Input/Output) pads are placed around the periphery (edge) of the die. They are the        communication bridge between the chip's internal logic and the outside world.

### ✋Macro Placement:

- Macros are large, pre-designed blocks like SRAM (memory), PLLs, or custom IP (Intellectual Property).

- Macros take up huge amounts of space and their placement is strategic: they should be placed close to the logic they communicate with to minimize wire length (using a guide called flylines), and they must be positioned to avoid congestion.


### 📱Standard Cell Row Creation:

- The core area is divided into horizontal rows where the standard cells (basic logic gates) will be placed and powered.

### 🪫Power Planning (PDN):

- This is highly critical! You must create the Power Distribution Network (PDN)—a grid of thick metal straps (VDD and GND)—to deliver stable power to every part of the chip. A weak PDN leads to IR Drop (voltage sag), which causes timing failures.

### 📱Adding Physical-Only Cells:

- Tap Cells (like the TAPCELL_X1 that caused your error) are special cells inserted into the standard cell rows to maintain substrate integrity and prevent latch-up.

- Endcaps are placed at the ends of rows.

- Blockages are defined to reserve areas for future logic or to keep standard cells away from macro pins to avoid congestion.

### 🩳Inshort A good floorplan minimizes wire length, balances power, and prevents congestion, making the subsequent steps of placement and routing much easier and faster to complete.


# 🅿️Placement 

- The main goals are to arrange all the standard cells (the basic logic gates like AND, OR, flip-flops) and smaller blocks within the core area defined during floorplanning, trying to achieve:

## 🔥so there are things we trying to achive 

- Minimize Wire Length: Place connected cells close together to keep the wires short. Shorter wires mean faster signals and less power consumption. 📏

- Reduce Congestion: Avoid packing too many cells into one area, which would make it impossible to route the wires later. 🚦

- Meet Timing: Ensure that placing cells doesn't create paths that are too long for signals to  travel within the required clock cycle time. ⏱️


## 🗃️files we needed for it

### 📚Placement tools need:

- Floorplan DEF/ODB: The output from the floorplanning stage, defining the core area, rows, macro locations, and I/O pins.

- Synthesized Netlist (.v): Describes which standard cells are used and how they are connected.

- Libraries (.lef, .lib): Provide the physical shapes (LEF) and timing information (LIB) for all standard cells. 

### satges of placement 

## 🌍↔️ Global Placement: 

- Goal: Find the approximate best location for every standard cell to minimize overall wire length (often using the HPWL metric you saw earlier).

- Process: Uses complex algorithms (like quadratic placement or partitioning). At this stage, cells might overlap or not be perfectly aligned to the rows. It prioritizes optimal positioning based on connections.

## 📏✅Detailed Placement (Legalization): 
 
- Goal: Take the rough locations from global placement and make them legal. This means snapping each cell precisely onto the standard cell rows defined in the floorplan and ensuring no cells overlap.

- Process: Makes small, local adjustments to cell positions while trying to preserve the wire length optimization achieved during global placement. It strictly adheres to the placement grid and design rules.


## now we will do the floorpalnning and placement in openroad.

### so I have done it for gcd_nangate45_clean.tcl
### file_1 for floorplanning

<img width="847" height="614" alt="Screenshot 2025-10-25 042652" src="https://github.com/user-attachments/assets/8a3d656f-5244-40bd-b2f7-fc2576c76f9e" />


### file_2 flow_floorplan.tcl

<img width="829" height="896" alt="Screenshot 2025-10-25 043003" src="https://github.com/user-attachments/assets/564d2889-d34f-4ef6-82b9-0c53e3944a83" />

### run this command in the tereminal 

```bash
openroad -gui -log gcd_logfile.log gcd_nangate45_clean.tcl 
```
<img width="1413" height="402" alt="Screenshot 2025-10-25 043547" src="https://github.com/user-attachments/assets/5778d02d-7308-4373-b69c-01614ee28b1a" />

### now it will open the openroad software

<img width="1852" height="1009" alt="Screenshot 2025-10-25 044028" src="https://github.com/user-attachments/assets/537dabc3-7e63-4490-8ca8-1cef47bb1848" />


## Obseravtions 
- The layout view shows a defined Die Area (outer white box) and Core Area (inner area with rows). Inside the core area, you can clearly see the horizontal Standard Cell Rows (green lines) have been created. This indicates the Floorplan Initialization stage is complete.

- in this we have the basic die core and rows get set .


## now we will run the next stage 

### file_4 flow_pdn.tcl

<img width="1317" height="890" alt="Screenshot 2025-10-25 044310" src="https://github.com/user-attachments/assets/30513068-5307-439a-9309-f7afbbb2712c" />

## now again if we run with the gcd_nangate45_clean.tcl


### power line(shown img)

<img width="1345" height="649" alt="Screenshot 2025-10-23 221602" src="https://github.com/user-attachments/assets/8be6d8f9-a933-48b8-b42c-f1a82c58b36f" />



### ground line (pink_line)

<img width="533" height="506" alt="Screenshot 2025-10-23 221614" src="https://github.com/user-attachments/assets/e2b6ab9d-ac41-454d-b181-7788d0ced47b" />

## Obseravtions

- In this we can see we have placed sucessfully power and ground lines on the chip.
- With the power infrastructure laid out, the standard cell rows (green/blue lines) now have access to power and ground. The design is structurally ready for the Placement stage, where the logic cells will be placed onto these rows and connected to these power lines.


## now our next step is the placement stage 

### file_4 flow_global_placement.tcl

<img width="1360" height="1003" alt="Screenshot 2025-10-25 045304" src="https://github.com/user-attachments/assets/6d3d8106-ebe8-403d-bb01-5e1d5f6e4826" />


<img width="1856" height="754" alt="Screenshot 2025-10-25 045329" src="https://github.com/user-attachments/assets/310c208c-c044-4ea4-b3f8-cc7dd1a78480" />


### reseult we get 

<img width="845" height="814" alt="Screenshot 2025-10-25 050318" src="https://github.com/user-attachments/assets/b1362a41-742b-40fb-a24b-284fd097e1f0" />



<img width="1856" height="1011" alt="Screenshot 2025-10-23 225225" src="https://github.com/user-attachments/assets/e2230332-a2b4-4855-8721-5f37d7712030" />

## Obseravtions 

- in this we can see that all the standered cells are placed but they are overlapping ,becuase we have not done yet the proper detailed placement

- there are the I/O pins at the sides of the chip ,it is like and small uppar part of arrow.
  
  - the standard cells (small red blocks) are now placed onto the horizontal rows within the core area. This confirms that both Global Placement and Detailed Placement (legalization) have finished. 

- The cells appear somewhat clustered towards the center and middle rows, leaving some rows less densely populated. This distribution is determined by the global placement algorithm trying to minimize wire length based on the netlist connections.


## now we will do the detailed placement



### file_5 flow_detalied_placement.tcl

<img width="967" height="641" alt="image" src="https://github.com/user-attachments/assets/ecc8d6d1-58d5-4475-a33f-a11f43e34b6a" />


### result we get

<img width="967" height="778" alt="Screenshot 2025-10-25 051321" src="https://github.com/user-attachments/assets/f6a2c71c-3f31-4239-9d6c-da8a3d5b8416" />




<img width="1851" height="1049" alt="Screenshot 2025-10-23 231413" src="https://github.com/user-attachments/assets/e640a19a-76ba-450e-a8d9-2a512dadc0cf" />


## Observations 

- in this we can see that standered cell are not overlapping as it was case in the previous image 
- The layout view clearly shows the standard cells (small red blocks) placed onto the horizontal standard cell rows (green/blue lines)

- Timing Analysis Results : Worst Negative Slack (WNS) for Setup Timing. Since it's positive (+0.106 ns), the design currently meets its setup timing requirements.

- This usually represents the worst Hold Slack. The small negative value (-0.009 ns) indicates very minor hold time violations. These are typically fixed later during clock tree synthesis (CTS) or optimization.





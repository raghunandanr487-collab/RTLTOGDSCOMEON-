- Fix up small DRC errors and verify the design is ready to be inserted into our flow.
- Save the finalized layout with custom name and open it.
Generate lef from the layout.
- Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
- Run openlane flow synthesis with newly inserted custom inverter cell.
- Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
- Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
- Do Post-Synthesis timing analysis with OpenSTA tool.
- Make timing ECO fixes to remove all violations.
- Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.-
Post-CTS OpenROAD timing analysis.
- Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.




 ### Fix up small DRC errors and verify the design is ready to be inserted into our flow.
Conditions to be verified before moving forward with custom designed cell layout:

- Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
- Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
- Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.
Commands to open the custom inverter layout

```bash
   # Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```
## Screenshot of tracks.info of sky130_fd_sc_hd


<img width="877" height="740" alt="Screenshot 2025-11-11 195405" src="https://github.com/user-attachments/assets/0aec5831-d2cf-4b72-a7c8-eeb32b02c651" />


```bash
   # Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```


<img width="929" height="788" alt="Screenshot 2025-11-11 195736" src="https://github.com/user-attachments/assets/1a64cd8d-335a-4fa1-b3b1-633931d327b6" />

### Condition 1 verified

<img width="876" height="669" alt="Screenshot 2025-11-11 200022" src="https://github.com/user-attachments/assets/8ba75e64-b419-4d34-bf88-3f53f71ab53b" />


### condition 2 verfied


<img width="872" height="590" alt="Screenshot 2025-11-11 201146" src="https://github.com/user-attachments/assets/8204c423-3b30-4103-aa79-5194a3b2af42" />


### this file is been created


<img width="938" height="782" alt="Screenshot 2025-11-11 201415" src="https://github.com/user-attachments/assets/b6113651-1421-4096-a2d3-f536eea14b9b" />



<img width="732" height="113" alt="Screenshot 2025-11-11 201754" src="https://github.com/user-attachments/assets/7be33c16-5fec-4154-bddd-cdeea1a75463" />


### Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
  
  - Commands to be added to config.tcl to include our custom cell in the openlane flow
```bash
   set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

### Run openlane flow synthesis with newly inserted custom inverter cell.
Commands to invoke the OpenLANE flow include new lef and perform synthesis

```bash
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

<img width="727" height="483" alt="Screenshot 2025-11-11 202218" src="https://github.com/user-attachments/assets/bfd02dd8-c4cd-412a-b29d-6dd7c6b3bed1" />


<img width="740" height="486" alt="Screenshot 2025-11-11 202405" src="https://github.com/user-attachments/assets/99724f5a-dfee-492c-8e70-7e54e31b30a1" />


<img width="727" height="481" alt="Screenshot 2025-11-11 202422" src="https://github.com/user-attachments/assets/386ad968-0eb8-4fe3-b28b-3b7c3ca34adf" />



### Commands to view and change parameters to improve timing and run synthesis


```bash
   # Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

## result


<img width="731" height="484" alt="Screenshot 2025-11-11 203449" src="https://github.com/user-attachments/assets/1b07652e-eb74-46a5-a684-992ff414627e" />

### nce synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

```bash
   # Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```


<img width="734" height="480" alt="Screenshot 2025-11-11 203614" src="https://github.com/user-attachments/assets/66cc7a03-a126-4ce9-8f2a-89519e4ccb53" />

### now we will run the placement 

##### we get 


<img width="728" height="492" alt="Screenshot 2025-11-11 203827" src="https://github.com/user-attachments/assets/58142997-10b8-4849-8b75-5107640606f7" />



<img width="879" height="775" alt="Screenshot 2025-11-11 212952" src="https://github.com/user-attachments/assets/c65eda74-f3f3-4153-a67c-c5b89b7d9ae9" />



















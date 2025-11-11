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



## Now we will see some theory

### Clock is distributed from a common source (CLK1) to two flip-flops (FF1 and FF2).

<img width="1821" height="878" alt="Screenshot 2025-10-31 124648" src="https://github.com/user-attachments/assets/d97ea5c2-8d1e-4b16-a412-c44c886028f9" />

-  The clock path to FF1 has a propagation delay t1, and the path to FF2 has a propagation delay t2.
 -  The difference between these two delays is called clock skew.

- Skew = t2 − t1

- If the clock arrives later at FF2 compared to FF1 (t2 > t1), the design experiences positive skew on that path.
-  The lower diagram shows data flowing from FF1 → logic → FF2.

- This is a typical sequential timing path.

- Clock skew affects both setup and hold timing:

- Positive skew helps setup timing (more time for data to travel)

- Positive skew hurts hold timing (data might reach too early)

- To ensure correct timing, the skew must be controlled through proper clock-tree design (CTS).
-  FF1 launches the data on the rising edge of its clock, and FF2 captures it on its (possibly skewed) rising edge.
-  The inverter and gate between FF1 and FF2 represent combinational logic delay, which must meet setup/hold constraints.

### Multiple flip-flops (FF1, FF2) are placed at different physical locations in the layout.
<img width="1860" height="968" alt="Screenshot 2025-10-31 125134" src="https://github.com/user-attachments/assets/b4c41cc3-b3bc-42fd-b5aa-487663b645ba" />




Each block has unique positions for FF1 and FF2, creating different distances from the clock source.

2. The clock signal cannot directly drive all these flip-flops because of:

Long wire lengths

High capacitance

Uneven delays

Risk of large clock skew

3. To fix this, Clock Tree Synthesis inserts buffers (Buf) on the clock network.

These buffers help distribute the clock evenly.

4. Every clock branch receives buffering so that the clock arrival time at each FF is balanced.
5. The yellow, purple, and blue lines represent various clock routing paths feeding different regions.
6. Buffers are inserted at key junctions to split the clock network (like branching a tree).
7. The goal is to ensure that:

Clock delay to each FF is almost equal

Clock skew is minimized

Timing requirements (setup/hold) are satisfied

8. The right-side block diagram shows the logical connectivity

— each Din input routes through logic and then into two flip-flops (FF1 → FF2).

9. CTS ensures that the clock for FF1 and FF2 in each data path arrives at nearly the same time.
10. The final result is a balanced, buffered, low-skew clock distribution network.


<img width="1822" height="828" alt="Screenshot 2025-10-31 131551" src="https://github.com/user-attachments/assets/4345c589-0a5f-4a2e-addf-e37e8ad1be6c" />


1. The clock network is modeled as a long RC (resistance–capacitance) structure.

Every metal wire has resistance (R) and every node adds capacitance (C).
This RC network slows down the clock as it travels.

2. As the clock travels through long paths, the signal rise/fall becomes slower.

The waveform becomes more “rounded” because the RC network filters the signal (low-pass effect).

3. The long, branching structure shown (purple wires + blue capacitors) represents the actual clock distribution path across the chip.

The vertical and horizontal routes

Buffers inserted at key points

Multiple capacitive loads at every flip-flop pin

4. The RC delay of the network is represented using a simple RC circuit (bottom-left).

This is an analogy:

R = wire resistance

C = load at each node (FF input, via, metal overlap)

5. The timing graph (bottom-right) shows how an RC network changes the signal:

The output voltage (Vout) rises slowly (not instantly)

Time constant τ = R × C controls how fast it reaches Vdd

Clock edges get delayed and become less sharp

6. These delays cause clock skew between flip-flops.

Some FFs receive the clock earlier than others due to different:

Wire lengths

Resistances

Capacitances

Routing patterns

7. The flip-flop diagram (right side) shows 4 different clock branches feeding 4 FF pairs (FF1 → FF2).

Each group of FFs sees its own clock path with unique delays.

8. Because each FF pair has a different RC delay on its clock line, skew is produced.

This impacts:

Setup timing (if clock arrives early)

Hold timing (if clock arrives late)

9. Clock tree synthesis (CTS) is required to fix this delay imbalance.

CTS uses:

Buffers

Load balancing

Path equalization

Controlled routing

10. The overall point:

Long interconnect + RC delay = distorted clock → skew between flip-flops → timing failures if not corrected.

### Clock Tree Synthesis (CTS) — Layout View + Logical View Explanation

<img width="1882" height="933" alt="Screenshot 2025-10-31 131955" src="https://github.com/user-attachments/assets/4974f598-e7f1-47f1-b5a3-9d427acf388d" />

1. The left side shows the physical layout after CTS.

This layout includes:

Flip-flops (FF1 and FF2) for each data path

Clock buffers (Buf) inserted to balance delays

DECAP cells (DECAP1, DECAP2) for stabilizing power rails

Clock routes highlighted in different colors (yellow, purple, black)

2. Each block of logic (like Block-A, Block-B, Block-C) has its own local clock path.

Because their positions are different, the wire length to each FF varies, leading to different clock arrival times.

3. CTS inserts buffers to equalize clock delay across all branches.

The red/yellow “Buf” cells are added automatically to:

Reduce RC delay

Strengthen long wires

Balance clock arrival time (reduce skew)

4. The colored groups represent different clock domains/branches.

Yellow group → DOUT1 path

Green/yellow → DOUT2

Blue → DOUT3

Green → DOUT4
Each group receives its own balanced clock tree.

5. DECAP cells placed near heavy switching regions help reduce IR drop.

CTS uses DECAPs around clock buffers because the clock network consumes high dynamic current.

6. The right-side image shows the logical connection diagram.

This includes:

Din inputs feeding FF1

Small logic (inverter, gate) between FF1 → FF2

Final Dout outputs from FF2

Clock signal routing (Clk1, Clk2, Clk Out) to each corresponding FF

7. Clock buffers ensure that FF1 and FF2 get the clock at nearly the same time.

This avoids timing issues like:

Setup violations

Hold violations

Uncontrolled skew

8. The objective of CTS shown here is to build a balanced, low-skew clock tree.

It ensures:

All flip-flops switch in sync

The system runs reliably at the target frequency

Clock jitter and voltage noise are minimized by DECAPs + buffers

9. Final outcome:

A well-optimized physical clock distribution network matching the logical design on the right.

### Impact of Crosstalk Delta Delay on Clock Skew
<img width="1858" height="1112" alt="Screenshot 2025-10-31 132435" src="https://github.com/user-attachments/assets/0fd2cbad-487a-49e3-bf0f-6bfe5fcd2faa" />

1. Crosstalk occurs when a switching aggressor net interferes with a nearby victim net.

The coupling capacitor Cm between wires injects noise and alters the delay of the victim path.

2. Before Crosstalk:

Victim path delay = D

3. After Crosstalk:

Victim path delay increases to D + Δ

Δ = extra delay caused by aggressor switching

4. In the clock network inside the chip:

Two clock branches, L1 and L2, originally had equal delay.

Due to crosstalk, the L2 branch delay becomes L2 + Δ

5. Clock Skew Introduced by Crosstalk

Clock skew = difference in arrival time between two clock branches:

Skew
=
𝐿
1
−
(
𝐿
2
+
Δ
)
Skew=L1−(L2+Δ)

If L1 = L2, then:

Skew
=
Δ
Skew=Δ

✅ Crosstalk directly adds skew to the clock network.

6. Why this is dangerous?

Extra skew can cause setup/hold violations

FFs may capture incorrect data

Chip timing becomes unpredictable

Worst-case: functional failure

7. The diagram shows:

Yellow dashed path = clock route affected by crosstalk

Its delay becomes L2 + Δ

Blue path = unaffected branch (delay = L1)

Result = clock imbalance → skew = Δ



### Timing Analysis With Real Clocks – Explanation
<img width="1871" height="1072" alt="Screenshot 2025-10-31 143934" src="https://github.com/user-attachments/assets/1397086d-a5dd-49e9-8a77-ba03600b4288" />


1. Real Clock Network Delays

Every clock path has:

Wire RC delay → delay due to wire resistance + capacitance

Buffer delay → delay added by clock tree buffers

These accumulate along each clock route.

✅ 2. Two Clock Paths: Δ₁ and Δ₂

The diagram highlights two main paths:

Δ₂ path (upper FF1 → FF2 cluster) includes:

Real wire RC delay 1

Buffer delay

Real wire RC delay 2

Buffer delay

Real wire RC delay 3

Buffer delay

Real wire RC delay 4

Buffer delay

Real wire RC delay 5

This is the total clock delay to the FFs feeding Dout1, Dout3, ClkOut.

Δ₁ path (lower FF1 → FF2 cluster) includes:

Real wire RC delay 1

Buffer delay

Real wire RC delay 2

Buffer delay

Real wire RC delay 3

Buffer delay

Real wire RC delay 4

Buffer delay

Real wire RC delay 5

This is the clock delay reaching Dout2 and Dout4.

✅ Both Δ₁ and Δ₂ contain multiple segments of wire delay + buffer delay, but their values differ because of different routing lengths.

✅ 3. Impact on Hold Time

Hold time check requires:

Θ
+
Δ
1
>
𝐻
+
Δ
2
+
𝐻
𝑈
Θ+Δ
1
	​

>H+Δ
2
	​

+HU

Where:

Θ = Data path minimum delay

Δ₁ = Launch clock delay

Δ₂ = Capture clock delay

H = FF hold requirement

HU = Clock uncertainty

✅ This means the launch clock must not arrive too early compared to the capture clock.

✅ 4. Why This Matters?

Because of real routing:

Clock arrival times at FFs are never identical

Differences cause clock skew

Skew directly influences setup and hold margins

Incorrect skew → timing violations → chip malfunction

✅ 5. Conclusion

This diagram shows that timing analysis must use the real post-CTS clock delays, not ideal clocks.
These real delays (Δ₁, Δ₂) determine:

Setup time safety

Hold time safety

Overall timing closure success

<img width="1871" height="1072" alt="Screenshot 2025-10-31 143934" src="https://github.com/user-attachments/assets/82391ec5-4494-46c0-b669-320c5e30e5f6" />









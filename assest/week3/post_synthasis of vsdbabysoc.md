 # ❤️ GLS OF BABYSOC
 
 ## 🎲 POST-SYNTHESIS SIMULATION 

 - Gate-Level Simulation is performed to validate the functionality of a design after synthesis.       RTL or behavioral simulations, which operate at a higher abstraction level, GLS works on the post-   synthesis netlist, containing the actual logic gates and their interconnections used in the final    implementation. It ensures that the synthesized design behaves as intended before moving to timing   analysis or fabrication.

   ### Key Points of Gate-Level Simulation (GLS) for BabySoC

   - Timing-Aware Verification:
 GLS uses Standard Delay Format (SDF) files to include real timing information, ensuring that       the SoC meets timing constraints. This helps verify that the design behaves correctly under        practical conditions.

 -  Post-Synthesis Design Validation:
Gate-Level Simulation confirms that the logical functionality of the design remains accurate after synthesis. It also helps detect potential issues such as glitches or metastability in the synthesized netlist.

-  Simulation Tools:
Simulators like Icarus Verilog (or similar) are used to compile and run the gate-level netlist, while waveforms are analyzed using tools like GTKWave.

- 4. Significance for BabySoC:
BabySoC integrates multiple modules, including the RISC-V processor, PLL, and DAC. GLS ensures that these modules work together correctly and adhere to timing requirements in the synthesized design
   

## here are some commands to do the postsynthasis 

#### 🥇first you have to start the yosys
#### insdie it you have read_verilog files rvmyth.v and clk_gate.v like inshown in the image
   
<img width="669" height="300" alt="Image" src="https://github.com/user-attachments/assets/6826529b-c193-4f5e-a7c0-9ace29489db9" />

<img width="677" height="168" alt="Image" src="https://github.com/user-attachments/assets/6f1d2e1c-2643-4816-b0c3-98b0dd4854b3" />

#### 🥈 now you have to read the liberty files like  shown in the image avsdpll.lib,avsddac.lib,sky130--lib


<img width="753" height="456" alt="Image" src="https://github.com/user-attachments/assets/7ab183b6-ef73-41d1-8d3c-96792afb7779" />




#### 🥉 after all doing this we will print the state image of it are 

<img width="431" height="289" alt="Image" src="https://github.com/user-attachments/assets/228143c4-e2cd-41fb-8a5c-30c19dd89682" />

<img width="549" height="573" alt="Image" src="https://github.com/user-attachments/assets/5c71d6e2-0996-497a-bbef-150f1820ff97" />


<img width="476" height="309" alt="Image" src="https://github.com/user-attachments/assets/34af402b-b21f-40f6-b6db-0d4ff2b0c059" />

<img width="629" height="670" alt="Image" src="https://github.com/user-attachments/assets/161b668d-85b7-4375-bba1-567029250f32" />

### 🌼 next step is to optimization and d flipflop mapping by using command dfflibmap -liberty /dierctory/

### 📈 another step is to clean or remove the unused cell

<img width="935" height="228" alt="Image" src="https://github.com/user-attachments/assets/bb7243b2-f1bf-43a6-a278-92233c63d4df" />

<img width="856" height="78" alt="Image" src="https://github.com/user-attachments/assets/20a3c46a-1a9c-4a24-89c7-5ca40503018b" />

- 💠 now if we write the state then it will print the state

 <img width="604" height="913" alt="Image" src="https://github.com/user-attachments/assets/20519e2b-6858-40f7-b4f9-4fcbbaf0b3c9" />

<img width="481" height="397" alt="Screenshot 2025-10-05 133953" src="https://github.com/user-attachments/assets/d64bbe13-051e-4f48-ab68-d6efb6ff25da" />

## ▶️POST_SYNTHESIS SIMULATION AND WAVEFORMS

#### 🥇 step compile thetestbench
 - Run the following iverilog command
```bash iverilog -o post_synth_sim.out \
-DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 \
-I /home/iamtheking/Desktop/vlsi/vsd/VSDBabySoC/src/include \
-I /home/iamtheking/Desktop/vlsi/vsd/VSDBabySoC/src/gls_model \
  vsdbabysoc.synth.v testbench.v```










  








 

 

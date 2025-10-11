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







 

 

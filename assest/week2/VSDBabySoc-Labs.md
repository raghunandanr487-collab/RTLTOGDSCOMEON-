

## Downlode

- for the simulation of the VSDBabySoc we have  to do multiple git cloning so we need 



VSDBabySoC/
├── src/
│   ├── include/
│   │   ├── sandpiper.vh
│   │   └── other header files...
│   ├── module/
│   │   ├── vsdbabysoc.v      # Top-level module integrating all components
│   │   ├── rvmyth.v          # RISC-V core module
│   │   ├── avsdpll.v         # PLL module
│   │   ├── avsddac.v         # DAC module
│   │   └── testbench.v       # Testbench for simulation
└── output/
└── compiled_tlv/         # Holds compiled intermediate files if needed


## 🛠️Cloning the Project
these are the following links 
### Vsdbabysoc.v (Top-Level SoC Module)
- This is the top-level module that integrates the rvmyth, pll, and dac modules.
  [VSDBabySoC](https://github.com/manili/VSDBabySoC.git)

### rvmyth.v(RISC-V Core)
- The rvmyth module is a simple RISC-V based processor. It outputs a 10-bit digital signal (OUT)   to be converted by the DAC.
   [rvmyth](https://github.com/kunalg123/rvmyth/)

### avsdpll.v (PLL Module)
- The pll module is a phase-locked loop that generates a stable clock (CLK) for the RISC-V core.
 [Introduction](https://github.com/ireneann713/PLL.git)&&&[avsdpll](https://github.com/lakshmi-sathi/avsdpll_1v8.git)

### avsddac.v(DAC Module)
- The dac module converts the 10-bit digital signal from the rvmyth core to an analog output.
[avsddac](https://github.com/vsdip/rvmyth_avsddac_interface.git)


AFTER ALL THIS INSTALLATION WE HAVE TO COVERT THE FILE OF RMYTH TO .V FILE SO WE NEED MORE PACKAGES TO INSTALL 


### First we need to install some important packages:

- $ sudo apt install make python python3 python3-pip git iverilog gtkwave docker.io
- $ sudo chmod 666 /var/run/docker.sock
- $ cd ~
- $ pip3 install pyyaml click sandpiper-saas

### second we can clone this repos in an arbitary directory

- $ cd ~
- $ git clone https://github.com/manili/VSDBabySoC.git

### third to make the pre_synth_sim.vcd:

- $ cd VSDBabySoC
- $ make pre_synth_sim

The result of the simulation (i.e. pre_synth_sim.vcd) will be stored in the output/pre_synth_sim directory.

now we will see the image of the 

- there are the two most imaportant signal are clk and out . clk is provided by the ppl and out 
  which is in blue colour wave it is the analog output of the DAC. 

- there are other signal also VREFH and VREFL ,REF signal is also there and VCO_IN signal is      trying to get syncronized with it ,once it get syncronized it locked it frequency to refence     ferquency


<img width="1503" height="1025" alt="Image" src="https://github.com/user-attachments/assets/7e99fb5f-6320-4b4a-87cc-5e75f2bfcce6" />

signal which are shown in this image are

- 🥇 CLK : it is the siganl which is commming from the ppl output .
- 🥈 D[9:0] : It is the signal of digital bits comes from the core .
- 🥉 OUT: It is the analog signal which cna simulate analog values.it is the output wire real             out signal of the Dac module . this signal comes from the DAC,originally.









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
This is the top-level module that integrates the rvmyth, pll, and dac modules.
[VSDBabySoC](https://github.com/manili/VSDBabySoC.git)

### rvmyth.v(RISC-V Core)
The rvmyth module is a simple RISC-V based processor. It outputs a 10-bit digital signal (OUT) to be converted by the DAC.
[rvmyth](https://github.com/kunalg123/rvmyth/)

### avsdpll.v (PLL Module)
The pll module is a phase-locked loop that generates a stable clock (CLK) for the RISC-V core.
[Introduction](https://github.com/ireneann713/PLL.git)&&&[avsdpll](https://github.com/lakshmi-sathi/avsdpll_1v8.git)

### avsddac.v(DAC Module)
The dac module converts the 10-bit digital signal from the rvmyth core to an analog output.
[avsddac](https://github.com/vsdip/rvmyth_avsddac_interface.git)


AFTER ALL THIS INSTALLATION WE HAVE TO COVERT THE FILE OF RMYTH TO .V FILE SO WE NEED MORE PACKAGES TO INSTALL 


### First we need to install some important packages:

- $ sudo apt install make python python3 python3-pip git iverilog gtkwave docker.io
- $ sudo chmod 666 /var/run/docker.sock
- $ cd ~
- $ pip3 install pyyaml click sandpiper-saas

### second we can clone this repos in an arbitary directory

















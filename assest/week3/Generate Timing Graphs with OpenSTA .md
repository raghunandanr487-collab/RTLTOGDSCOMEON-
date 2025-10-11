## ✈️ generating  the timing analysis and graphs through OpenSTA


### first we have to install the OpenSTA

```bash
# On your Home Directory type the following command
sudo apt-get update
sudo apt-get install build-essential tcl-dev tk-dev cmake git

# Clone the OpenSTA repository by executing the following command:
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
```
### YOU can also follow the link and can downlode the opensta

-  https://github.com/parallaxsw/OpenSTA.git


### now we will one exmple of it 

#### follow the images which i have shown 

  in this we have read the liberty files and verilog file and link it to top desgin

<img width="955" height="808" alt="Screenshot 2025-10-09 235738" src="https://github.com/user-attachments/assets/a619eb44-461f-44fe-8fbb-141fb8960392" />

 <img width="700" height="436" alt="Screenshot 2025-10-09 154405" src="https://github.com/user-attachments/assets/249286bf-0211-4a58-94a7-d2f31cf06b35" />

   
  #### In this we get the state
     
<img width="798" height="510" alt="Screenshot 2025-10-09 154417" src="https://github.com/user-attachments/assets/257a488c-bc98-4d31-ac7a-fa268e359f96" />


## now we will do for vsdbabysoc

### so we need some installation 

```BASH
# To begin, clone the VSDBabySoC repository using the following command:
git clone https://github.com/manili/VSDBabySoC.git
```

### timing libraries

```BASH
The timing libraries can be downloaded from:
https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing
```
### git cannot clone the subdirectory so do this 

```bash
git clone --no-checkout https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd.git
cd skywater-pdk-libs-sky130_fd_sc_hd
git sparse-checkout init --cone
git sparse-checkout set timing
git checkout
```
### vsdbabysoc sdc scripit 
```bash
set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period 11
```

### so we need the tcl scripit for this 

```bash
 set list_of_lib_files(1) "sky130_fd_sc_hd__tt_025C_1v80.lib"
 set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v65.lib"
 set list_of_lib_files(3) "sky130_fd_sc_hd__ff_100C_1v95.lib"
 set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
 set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
 set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
 set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
 set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
 set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
 set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
 set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
 set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
 set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v76.lib"
```

## In this way i have wote my files 


```bash
# === Read Custom Block Libraries ===
read_liberty /data/Desktop/vlsi/vsd/VSDBabySoC/src/lib/avsddac.lib
read_liberty /data/Desktop/vlsi/vsd/VSDBabySoC/src/lib/avsdpll.lib


# === Create Output Directory if Missing ===
exec mkdir -p /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT


# === Loop Through Each Process Corner Library ===
for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {

    puts "\n=== Running STA for $list_of_lib_files($i) ==="

    # Read standard cell library (from timing folder)
    read_liberty /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/timing/$list_of_lib_files($i)

    # Read synthesized Verilog netlist
    read_verilog /data/Desktop/vlsi/vsd/VSDBabySoC/src/module/vsdbabysoc.synth.v

    # Link the design
    link_design vsdbabysoc
    current_design

    # Apply constraints
    read_sdc /data/Desktop/vlsi/vsd/VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc

    # Perform setup checks
    check_setup -verbose

    # === Generate Reports ===

    # Detailed min-max delay report
    report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} \
        > /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/min_max_$list_of_lib_files($i).txt

    # Worst MAX slack report
    exec echo "\n$list_of_lib_files($i)" >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_worst_max_slack.txt
    report_worst_slack -max -digits {4} >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_worst_max_slack.txt

    # Worst MIN slack report
    exec echo "\n$list_of_lib_files($i)" >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_worst_min_slack.txt
    report_worst_slack -min -digits {4} >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_worst_min_slack.txt

    # Total negative slack report
    exec echo "\n$list_of_lib_files($i)" >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_tns.txt
    report_tns -digits {4} >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_tns.txt

    # Worst negative slack report
    exec echo "\n$list_of_lib_files($i)" >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_wns.txt
    report_wns -digits {4} >> /data/Desktop/vlsi/vsd/skywater-pdk-libs-sky130_fd_sc_hd/STA-OUTPUT/sta_wns.txt
}
```

### these are my files which i have generated


<img width="547" height="642" alt="image" src="https://github.com/user-attachments/assets/ee6207bd-b443-4252-bdf8-bc9edd622197" />


| **Library Corner**                | **Worst Setup Slack (WNS)** | **Worst Hold Slack (Min Slack)** | **Worst Setup Slack (Max Slack)** | **Total Negative Slack (TNS)** |
| --------------------------------- | --------------------------- | -------------------------------- | --------------------------------- | ------------------------------ |
| sky130_fd_sc_hd__tt_025C_1v80.lib | 0.0000 ns                   | 0.3096 ns                        | 1.8865 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ff_100C_1v65.lib | 0.0000 ns                   | 0.2491 ns                        | 3.7904 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ff_100C_1v95.lib | 0.0000 ns                   | 0.1960 ns                        | 5.3898 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ff_n40C_1v56.lib | 0.0000 ns                   | 0.2915 ns                        | 0.9227 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ff_n40C_1v65.lib | 0.0000 ns                   | 0.2551 ns                        | 2.4592 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ff_n40C_1v76.lib | 0.0000 ns                   | 0.2243 ns                        | 3.7081 ns                         | 0.0000 ns                      |
| sky130_fd_sc_hd__ss_100C_1v40.lib | -12.7117 ns                 | 0.9053 ns                        | -12.7117 ns                       | -9544.7930 ns                  |
| sky130_fd_sc_hd__ss_100C_1v60.lib | -4.9864 ns                  | 0.6420 ns                        | -4.9864 ns                        | -3424.7075 ns                  |
| sky130_fd_sc_hd__ss_n40C_1v28.lib | -56.3915 ns                 | 1.8296 ns                        | -56.3915 ns                       | –                              |
| sky130_fd_sc_hd__ss_n40C_1v35.lib | -36.3514 ns                 | 1.3475 ns                        | -36.3514 ns                       | –                              |
| sky130_fd_sc_hd__ss_n40C_1v40.lib | -27.7760 ns                 | 1.1249 ns                        | -27.7760 ns                       | –                              |
| sky130_fd_sc_hd__ss_n40C_1v44.lib | -23.6693 ns                 | 0.9909 ns                        | -23.6693 ns                       | –                              |
| sky130_fd_sc_hd__ss_n40C_1v76.lib | -5.8387 ns                  | 0.5038 ns                        | -5.8387 ns                        | –                              |








  


  






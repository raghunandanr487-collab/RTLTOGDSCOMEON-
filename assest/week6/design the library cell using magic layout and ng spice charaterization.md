
## design library cell using magic layout 

- Clone custom inverter standard cell design from github repository: Standard cell design and characterization using OpenLANE flow.
- Load the custom inverter layout in magic and explore.
- Spice extraction of inverter in magic.
- Editing the spice model file for analysis through simulation.
- Post-layout ngspice simulations.
- Find problem in the DRC section of the old magic tech file for the skywater process and fix them.


```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

## results
<img width="709" height="803" alt="Screenshot 2025-10-31 181759" src="https://github.com/user-attachments/assets/1ad9f43d-9b00-4f5d-aae4-04e5734324b5" />

<img width="734" height="797" alt="Screenshot 2025-10-31 181649" src="https://github.com/user-attachments/assets/0fa0df60-5389-444b-aad3-d156a807e05b" />

<img width="850" height="340" alt="Screenshot 2025-10-31 182235" src="https://github.com/user-attachments/assets/7e63f2c4-b7d0-4c4b-b53d-06a1482fcfce" />


###  Spice extraction of inverter in magic.
Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```bash
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
## this file will be created and we will update it

<img width="946" height="1038" alt="Screenshot 2025-11-11 160604" src="https://github.com/user-attachments/assets/cbb24d50-7a69-4845-b70f-3b76691cd393" />


### now we will do the spice simulation

<img width="730" height="485" alt="Screenshot 2025-11-11 160911" src="https://github.com/user-attachments/assets/a9d1b74b-46e0-475b-97c5-e6c16f314af8" />

## results 

<img width="903" height="1020" alt="Screenshot 2025-11-11 161018" src="https://github.com/user-attachments/assets/bf1d3b09-d322-467e-bbca-3677f951c3e8" />


<img width="1776" height="989" alt="Screenshot 2025-11-11 161109" src="https://github.com/user-attachments/assets/d0a6143d-f9e7-4450-8fc0-e9114de3cbf6" />































































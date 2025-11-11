
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


<img width="876" height="1021" alt="Screenshot 2025-11-11 161422" src="https://github.com/user-attachments/assets/11d5804b-f316-4e0c-9c20-c514f2aa5f32" />




<img width="799" height="960" alt="Screenshot 2025-11-11 161656" src="https://github.com/user-attachments/assets/4ee405e8-5f4a-4a98-9fa5-4c0d523bec13" />

## results






## Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

- Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

  ```bash
        # Change to home directory
  cd

  # Command to download the lab files
  wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

  # Since lab file is compressed command to extract it
  tar xfz drc_tests.tgz

   # Change directory into the lab folder
   cd drc_tests

  # List all files and directories present in the current directory
   ls -al

   # Command to view .magicrc file
     gvim .magicrc

  # Command to open magic tool in better graphics
  magic -d XR &
  ```

## this is the file 
<img width="894" height="1026" alt="Screenshot 2025-11-11 164450" src="https://github.com/user-attachments/assets/f5dc72cb-e7e4-4153-9fa7-09826b6e9b40" />

 ### after running this we get 

<img width="909" height="1031" alt="Screenshot 2025-11-11 165330" src="https://github.com/user-attachments/assets/cf743a56-a4bf-45b3-b87b-60e90e737344" />



<img width="1435" height="806" alt="Screenshot 2025-11-11 170122" src="https://github.com/user-attachments/assets/b5131437-da45-49da-9b6c-3793d828d64a" />

### error 
<img width="708" height="608" alt="Screenshot 2025-11-11 190942" src="https://github.com/user-attachments/assets/6a0791be-da4f-4259-805b-89e243a6ef44" />

<img width="878" height="335" alt="Screenshot 2025-11-11 191021" src="https://github.com/user-attachments/assets/8d82baca-baea-4231-ad34-f3541aaefaa7" />

## another file 

<img width="656" height="500" alt="Screenshot 2025-11-11 193849" src="https://github.com/user-attachments/assets/8a84d6c5-95cd-4525-a306-c4268a8d9d10" />

```bash
   # Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```
<img width="880" height="673" alt="Screenshot 2025-11-11 194234" src="https://github.com/user-attachments/assets/79779416-cc9a-4b79-84d4-8c118636d4b9" />







  























































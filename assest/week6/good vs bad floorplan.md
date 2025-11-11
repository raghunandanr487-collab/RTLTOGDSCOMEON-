## FLOORPLANING 


- IN THIS WE DIRECTLY LODE THE FILES AND LODE IN THE MAGIC
  
- HERE ARE THE IMAGES OF IT 


### commands we will be use are these 

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```


## files we will use 

<img width="927" height="1020" alt="Screenshot 2025-10-29 201753" src="https://github.com/user-attachments/assets/008937ee-55f1-40cb-832b-8399b97e7845" />

<img width="877" height="1007" alt="Screenshot 2025-10-30 201831" src="https://github.com/user-attachments/assets/de50c44f-14bc-4fca-b6d8-8a74e6bc5143" />

## results


<img width="1848" height="993" alt="Screenshot 2025-10-30 224904" src="https://github.com/user-attachments/assets/d9255aae-8ab4-4574-b2c5-5c3a710f0dfd" />

<img width="1839" height="985" alt="Screenshot 2025-10-30 225444" src="https://github.com/user-attachments/assets/6a2ec203-b7ad-4f61-8cf7-cc537336733e" />

<img width="1853" height="989" alt="Screenshot 2025-10-30 230506" src="https://github.com/user-attachments/assets/f13d99ed-5143-44bb-8bc1-46adffc93d4c" />

<img width="1841" height="986" alt="Screenshot 2025-10-30 231425" src="https://github.com/user-attachments/assets/3ecfa71f-cdac-4358-9284-ad78f4405a9b" />





### now we will do placement 

- for doing placement we have tpo use the command 

```bash
# Congestion aware placement by default
run_placement
```

## Results

<img width="1834" height="971" alt="Screenshot 2025-10-31 174317" src="https://github.com/user-attachments/assets/43a055a8-84d9-4c2f-8db6-3446b0e2e6c4" />

<img width="1824" height="943" alt="Screenshot 2025-10-31 174334" src="https://github.com/user-attachments/assets/d755aa37-12db-4efd-8168-359aec6b6f1f" />


## now we will see some theory





- The cell design flow starts with inputs from the PDK (Process Design Kit).

- PDK includes DRC rules, LVS rules, SPICE models, and technology files.

- These rules define minimum feature sizes, spacing requirements, and device parameters.

- Lambda-based (λ) design rules are used to simplify layout constraints.

- Designers use this information to create layout geometries that meet all manufacturing rules.

- The technology file guides tools on layer properties, colors, connectivity, and allowed structures.

- All layout shapes must follow DRC to ensure the chip is fabrication-ready and error-free.

















## 🙃FLOORPLANING 


- IN THIS WE DIRECTLY LODE THE FILES AND LODE IN THE MAGIC
  
- HERE ARE THE IMAGES OF IT 


### commands we will be use are these 

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```


## 🗃️ files we will use 

<img width="927" height="1020" alt="Screenshot 2025-10-29 201753" src="https://github.com/user-attachments/assets/008937ee-55f1-40cb-832b-8399b97e7845" />

<img width="877" height="1007" alt="Screenshot 2025-10-30 201831" src="https://github.com/user-attachments/assets/de50c44f-14bc-4fca-b6d8-8a74e6bc5143" />

## 🍬results


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

## 🍬 Results

<img width="1834" height="971" alt="Screenshot 2025-10-31 174317" src="https://github.com/user-attachments/assets/43a055a8-84d9-4c2f-8db6-3446b0e2e6c4" />

<img width="1824" height="943" alt="Screenshot 2025-10-31 174334" src="https://github.com/user-attachments/assets/d755aa37-12db-4efd-8168-359aec6b6f1f" />


## 🙃🖤now we will see some theory

![WhatsApp Image 2025-11-11 at 15 14 57_1e5e5880](https://github.com/user-attachments/assets/2d0bd447-0497-495c-bb18-87a06b4be39b)


![WhatsApp Image 2025-11-11 at 15 14 56_355b4827](https://github.com/user-attachments/assets/9d4bf8d9-e635-4dd8-b33d-f3c568d6bd0c)



- The cell design flow starts with inputs from the PDK (Process Design Kit).

- PDK includes DRC rules, LVS rules, SPICE models, and technology files.

- These rules define minimum feature sizes, spacing requirements, and device parameters.

- Lambda-based (λ) design rules are used to simplify layout constraints.

- Designers use this information to create layout geometries that meet all manufacturing rules.

- The technology file guides tools on layer properties, colors, connectivity, and allowed structures.

- All layout shapes must follow DRC to ensure the chip is fabrication-ready and error-free.


### Cell Design Flow – Logic to Layout


<img width="1206" height="540" alt="image" src="https://github.com/user-attachments/assets/25901ea0-f615-4f43-a3a7-c6616c5ab3f9" />


###Cell Design Flow – Logic to Layo

The layout design of a standard cell begins with the transistor-level circuit, representing the logic function using PMOS and NMOS networks.

These transistor networks are often converted into Euler paths and stick diagrams to simplify the layout routing and ensure an optimal, compact structure.

The Process Design Kit (PDK) provides essential inputs such as DRC rules, LVS rules, SPICE models, and library specifications, guiding the layout engineer.

The design process includes circuit design, layout creation, and cell characterization, ensuring the cell meets functional and timing requirements.

The final output of the cell design flow is a CDL (Circuit Description Language) file, which accurately represents the transistor connections for verification and integration.



![WhatsApp Image 2025-11-11 at 15 14 53_d2ca8898](https://github.com/user-attachments/assets/a6af67cc-408c-41ea-a880-32af62f71330)


- The layout of a CMOS logic cell is optimized using Euler paths, which provide the best ordering of transistors to minimize routing complexity.

- By creating Euler paths for both the PMOS and NMOS networks, designers can align diffusion regions, reduce breaks, and make the layout more compact.

- The stick diagram visually represents transistor connections (poly, diffusion, metal) before creating the actual layout, helping to plan the structure efficiently.

- Using the optimized ordering (e.g., A–C–E–F–D–B), the resulting cell layout achieves fewer vias, fewer diffusion breaks, and more regular geometry, which improves performance and manufacturability.

- This process forms a critical part of the cell design flow, allowing the final standard cells to meet electrical, physical, and design-rule requirements.


![WhatsApp Image 2025-11-11 at 15 14 51_b26499c8](https://github.com/user-attachments/assets/84d50dbf-833b-4180-a258-f229440b88fb)



## 📉graph


![WhatsApp Image 2025-11-11 at 15 14 50_d8c7ba2b](https://github.com/user-attachments/assets/b0cf8075-de96-402e-a6fb-8144cfbd54e6)

### Timing Characterization – Thresholds and Slew Measurement

- Timing characterization defines how fast a cell responds to input changes by measuring threshold voltages during rising and falling transitions.

- The slew thresholds (slew_low_rise_thr, slew_high_rise_thr, etc.) mark specific voltage points on the input/output waveform used to calculate the slew rate—the transition speed of a signal.

- Similarly, in_rise_thr and in_fall_thr indicate the voltage levels used to detect when an input has effectively switched.

- out_rise_thr and out_fall_thr represent the points where output timing (propagation delay) is measured.

- By analyzing these points on the waveform, the cell’s delay, rise time, fall time, and slew can be accurately characterized for use in timing libraries.















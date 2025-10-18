
# POWER SUPPLY SCALING 


<img width="1739" height="589" alt="Screenshot 2025-10-18 211957" src="https://github.com/user-attachments/assets/d488fa89-89a6-448d-9f0f-b75ef334f555" />

- now we will see what happens if we reduce the power supply or in other sens if we reduce the vdd
 so what will happens

- in this image is shown  we have reduce the vdd from 2.5v to 1v keeping the the length and width constsnt


# spice simulation

## this is the file which have use

<img width="1814" height="915" alt="Screenshot 2025-10-18 212632" src="https://github.com/user-attachments/assets/879b06fd-9f22-4f45-8cc1-1052c453e5bf" />


## graph 

<img width="1820" height="932" alt="Screenshot 2025-10-18 185146" src="https://github.com/user-attachments/assets/4ff8db84-9167-46b0-852a-414feec616ed" />


## observations 

- in this we can see we have reduce the vdd
- we have the total six outputs
- so now we will see the advantges and disadvantages
  


## table

| **Aspect**                   | **Advantage (✅)**                                                                    | **Disadvantage (❌)**                                                                         |
| ---------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| **Power Consumption**        | ↓ Reduces dynamic power (`P = α·C·VDD²·f`) — lower energy usage and heat generation. | –                                                                                            |
| **Leakage Power**            | ↓ Reduces subthreshold leakage current, improving standby power efficiency.          | –                                                                                            |
| **Speed / Delay**            | –                                                                                    | ↑ Increases propagation delay (slower operation) because transistor drive current decreases. |
| **Noise Margin**             | –                                                                                    | ↓ Noise margin reduces — circuit becomes more sensitive to noise and less reliable.          |
| **Switching Threshold (Vm)** | –                                                                                    | Shifts closer to mid-supply; may cause improper logic levels in cascaded stages.             |
| **Output Swing**             | –                                                                                    | Output high and low levels may degrade, causing poor logic level separation.                 |
| **Static Behavior**          | –                                                                                    | Inverter transfer curve becomes less steep → reduced gain and weaker switching.              |
| **Reliability / Stability**  | ↓ Lower VDD reduces device stress and improves long-term reliability.                | –                                                                                            |































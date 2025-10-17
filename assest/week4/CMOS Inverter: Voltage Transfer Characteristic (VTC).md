
# 🖤 CMOS Inverter 
**Definition:**
The **Voltage Transfer Characteristic (VTC)** of a CMOS inverter is a graph that shows how the **output voltage changes** when the **input voltage** is increased from 0 to 🔋 (supply voltage).

It helps us understand how the inverter switches from logic HIGH to logic LOW. When the input is 0 V, the output is at 🔋 (logic 1), and when the input is at 🔋, the output becomes 0 V (logic 0). The middle part of the curve shows the transition region where both PMOS and NMOS are active.



  ## so now we will the image of the cmos invertor

  <img width="436" height="568" alt="image" src="https://github.com/user-attachments/assets/044844aa-3437-4651-b47e-2e0c12303074" />


   -  as you can this is teh invertor there is pmos and nmos
   -  this transistor will act like the switch when infinite off resistance when vgs<vt


 ##  now we will see the image 

   ![WhatsApp Image 2025-10-17 at 12 01 48_738e43cf](https://github.com/user-attachments/assets/653cd798-079e-4b8a-a919-526d3cf3852e)


- for the condition to on the pmos -vgs<-vt
- and for nmos vgs>vt
- now we will see the another image in which we will see how to on the cmos 
  
## here is the image

![WhatsApp Image 2025-10-17 at 12 09 17_c0c6f3bd](https://github.com/user-attachments/assets/d379f340-aaa1-42fb-bb15-88098aab4dec)

-  now if the vin is zero then vin -vdd =-vdd
-  so pmos will get on and nmos will get off
-  if the vin is  there  at the input  then noms will get on and pmos will get off

## now we will see the another image in which now it look like when pmos is on and nmos 

![WhatsApp Image 2025-10-17 at 12 18 38_66140a0f](https://github.com/user-attachments/assets/d2a23e3e-3b44-48a9-83d2-d7625598d551)

  - in this we can see that when vin =vdd capacitor is fully charged and direct path exist between vout and vss resulting in vout =0
  - when vin=0 direct path exist between vdd and vout resulting vout=vdd.
    


## now we will see the image of the graph

![WhatsApp Image 2025-10-17 at 14 19 43_795dae18](https://github.com/user-attachments/assets/87ffbfaf-b452-458a-b325-5c6e9acae439)

- as we can see the graph on the right side there is graph of pmos and at the left side the
   graph of the nmos
- the nmos graph we have seen previsously whcih is same IDSN VS VDSN
- so in pmos graph we can see that when the -vgs is increasing then neg of IDS  is also increasing
- so now we will convert this graph to another graph that i will shown in the image

  ## so here is the image


  ![WhatsApp Image 2025-10-17 at 14 47 50_c6b4399e](https://github.com/user-attachments/assets/7b75e309-679e-4240-a806-76e0fd26e455)


 - so here what we have to do that we have wrote the vin=vgs+vdd.
 - on the diif vgs we get the value of vin and then we have make the graph of it
 - graph is still vds vs IDSN but we have taken graph to positive y axis.

   ## now for the further econversion of graph we take it to positive x axis so we will the another image


 ![WhatsApp Image 2025-10-17 at 14 52 26_45524b15](https://github.com/user-attachments/assets/49a9435a-5059-4bed-b84b-c65fd013b26f)

- in this image we can see we usees the eauation of vout=vdd+vdsp
- after this we get the graph and it shows that capacitor is fully charged when the vin=0
- this called the load curve graph for pmos transistor
- now we will superimpose both the graph and find the vlotage transferr characterstics


   <img width="316" height="194" alt="image" src="https://github.com/user-attachments/assets/a5bc5ab8-9601-45a1-9350-65e8bb89ecf8" />

- by this grph we will plot the vtc graph by looking at the intersection of the graph


## so the VTC graph will look like this 

  <img width="500" height="300" alt="image" src="https://github.com/user-attachments/assets/ccdc1807-540d-461b-bd68-9fd09464b047" />

  - this graph will tell you about the pmos and nmos state at which voltage (vin), both  to of  them are in which state 
 - one of the observation of the graph is how there is drastically the vu decreases when we
   just increase the Vin by some amount
 - we can also find the voltage where the invertor swithes it values by drawing the line of 45 degree , where it cut the graph ,it will the vm voltage the
     invertor switches the value

## I have done the spice simulation and get the result like 

<img width="978" height="780" alt="Screenshot 2025-10-16 200023" src="https://github.com/user-attachments/assets/f9ddcef0-15e8-4898-89ba-dbb8183506cf" />

  




  ## what happen if  I chnage the value of w/l ?

- so the next thing is that we have to find the Wp/ LP / Wn/Ln ratio  so that we can identify how much should pmos greater than nmos
- so we have to derive some equations for this review we will directly see the equation for now


## here are the equations

![WhatsApp Image 2025-10-17 at 15 48 04_d1a6651f](https://github.com/user-attachments/assets/4913484c-1016-46d5-9ca9-a5ed8af4ecc4) 

- so we can see the equation here, Hindi question all are constant only Vm is vary or we have to plug Vm value
- as we see previously Vm  is the point where vin is equals to vout, where inverter switches its value.
- next part is to find the rise and fall delay

### rise delay
- it is the time in which capacitor get charged is called rise delay.

### fall delay
- it is the time in which capacitor get discharge.

## so to find the rice delay and fall delay we will superimpose the pulse in this spice simulation

### so this is the file we have choose


<img width="1463" height="993" alt="Screenshot 2025-10-16 192234" src="https://github.com/user-attachments/assets/858662c7-4dc2-4a38-a19a-09f36c06849e" />

### In the file we can see the pfet  width  is double off nfet 

## now we will see the graph of it vout vs time imposed on pules 

<img width="1482" height="963" alt="Screenshot 2025-10-16 192119" src="https://github.com/user-attachments/assets/fae13417-0419-47a6-8146-1fbd8c5f3532" />


### we can see here there is pulse in blue colour and vout in red colour soo for the rise delay we have to see at mid point of the red line where it is raising 

### so for the fall dealy we have to look at the point where the red line is falling , at it mid point  like this 

  ## rise dealy


  <img width="694" height="535" alt="Screenshot 2025-10-16 201640" src="https://github.com/user-attachments/assets/341ce00f-855b-4b52-8067-1b9bdb91fc12" />

  <img width="342" height="63" alt="Screenshot 2025-10-16 192052" src="https://github.com/user-attachments/assets/3ac3aead-1ded-4542-9237-471976824b71" />


## fall dealy 

<img width="618" height="529" alt="Screenshot 2025-10-16 201947" src="https://github.com/user-attachments/assets/e61ddbb6-1526-47cc-8657-53889eba5c36" />


#  Results

- rise dealy =2.48ns - 2.15ns
- fall dealy =4.33ns - 4.0521ns


# table and observations 

| Sr. No | VDD (V) | Rise Delay (ps) | Fall Delay (ps) | Vm (V) |
| :----: | :-----: | :-------------: | :-------------: | :----: |
|    1   |   1.2   |        44       |        71       |  0.94  |
|    2   |   2.0   |        68       |        80       |  1.25  |
|    3   |   2.4   |        45       |        84       |  1.35  |
|    4   |   5.0   |        37       |        89       |  1.40  |

- As we can see, there is very little change in Vm, which is an advantage for us.

- During fabrication, if there is any delay (for example, 2.45 µm), the value of Vm will not change much.

- Both rise delay and fall delay are important for maintaining proper clock (CLK) timing in downstream cells.

- One of the most important uses of these parameters is to study the delay behavior under different conditions.

###  If the Cell Delay is High

- If the cell delay is much higher and it violates the rule, then it results in negative slack.

- To correct this, we can use cells that have lower delay values (for example, 24 ps or 45 ps) to reduce the total cell delay and meet the timing requirements.

### example of any cell  
  Setup Time  = 0.30 ns
 Clock Delay = 0.45 ns
  ALU Delay   = 1.60 ns


















   














   






  




 

   





  


  

















  


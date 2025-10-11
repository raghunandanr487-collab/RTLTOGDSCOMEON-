## ⚛️ IMPORTANT POINT OF STA 

### ♟️ first we will the see the image of the launch and capture filp flop


<img width="600" height="242" alt="image" src="https://github.com/user-attachments/assets/9ab2f8db-34f5-472a-9dba-d5774663cfa1" />


- as we can see there are the two ff one is for launch and othe own is for the capture ff
- as we can see here there are the four timing paths and we consdier the timing path as flop clk in/input port and end point - flop d pin/output port

##### 🅰️ Arrival time 

- it means that the signal arrives at which time after the clock edge that lunched it.
- if the clk time period is of 1ns and it arrives at 0.8ns and that 0.8ns is arrival time.
  
#### ®️ Required time 

- the latest time by which the signal must arrive at point to meet the timing reqirnments.
- RT= CLOCK TIME -SETUP TIME .

#### 🏆 Slack
- it is the reqire time - arrival time for the hold analiysis so it should be positive(hold analysis)
- it should be positive ➕ for met timing reqiurnment


#### ♈ hold and setput
- SETUP(max delay) : Latest time by which data must arrive before the next active clock edge
- HOLD(min dealy): Earliest time after the clock edge that data must remain stable



### types of timing analysis
  
  #### 1. 🧜‍♂️ reg to reg
  #### 2. 🐪 in2reg
  #### 3. 🍬 reg2out
  #### 4. 🐼 in2out

## so i hav edone the reg2reg analysis only so now we will see the path based analysis

  ![WhatsApp Image 2025-10-11 at 18 07 34_5d5dbec1](https://github.com/user-attachments/assets/c92fb537-6677-43b2-886c-766a812dbbe9)



##### in the image you can see the worst case path and best case path so in hold analysis we take 
the best case path and you can also see the arrival time and reqire time and slack and 
##### ⚫ circle one is the delay of the cell and wire have other delay also   

 
#### 🧮 :for mroe accurate timing analysis we do pin node convantion in whhich we covert the cell delay 

![WhatsApp Image 2025-10-11 at 18 22 29_0c8860b7](https://github.com/user-attachments/assets/3f5f8e67-a093-46d6-bb72-9d3c1052c5f9)


### ⏰ SETUP TIME 

- In one line it is means that capture ff hsa safficeint time to see the data before the capture clk comes.


### 🫥 Negative latch 
  - A negative latch passes input to output when the clock is LOW
  - the image will show the tht it will get on when clk is zero

 
![WhatsApp Image 2025-10-11 at 18 27 35_5c5494c7](https://github.com/user-attachments/assets/60688bd2-932e-46e0-9dbd-69abcf7ca1f2)


### :🔮 Positive latch

- A positive latch passes input to output when the clock is HIGH

- image of it


![WhatsApp Image 2025-10-11 at 18 29 20_2fb9576f](https://github.com/user-attachments/assets/16fedefb-fad1-4f62-93c2-208f7d5d910d)


### 👟 filp flop

 - Combination of Master (Negative latch) and Slave (Positive latch)
 - in the image you can see it

   ![WhatsApp Image 2025-10-11 at 18 31 39_df54b59d](https://github.com/user-attachments/assets/f26c2d4c-1db2-49d9-a93a-1ee1d067a4bc)

- Ideal Clock: Slew is zero, ie, the Rise/Fall transitions are equal to zero

- Positive-edge FF: Implemented via master–slave configuration

- Setup time: Time before the rising clock edge during which D must be stable for correct Q output.

- CLK-Q delay: Time taken for Qm to propagate to Q includes transmission gate and inverter delay.

- Hold time: Duration D must remain valid after the clock edge; here, hold time is zero since D can change immediately after rising edge.


### 🉐 jittervaules

- jitter : it is the random vartion of clk edge timing
- it is comes to the power supply variation and voltage drop


   ![WhatsApp Image 2025-10-11 at 18 40 32_4edcef23](https://github.com/user-attachments/assets/36eefc35-0faf-439b-bb8d-eceb76e68f05)

- we can the see the noise margein is the amount of distortion is allowed
- there is an uncertain time also tht account for jitter and noise
  
  
### 🧑 on chip verification and variation

- on chip there will be not the smooth graph we get we get the diverted graph if there are the set of inverters

- like in the image i have shown

  ![WhatsApp Image 2025-10-11 at 18 47 00_3538f942](https://github.com/user-attachments/assets/a59ea3ae-a803-43cc-9871-8c87fbeb0b68)


- so it can be fix by the clk pull in and clk pull out

## 🚛 so in the next images i have shown how actuly it can be done clk pull in and clk pull out

![WhatsApp Image 2025-10-11 at 18 49 23_1ce1c8c1](https://github.com/user-attachments/assets/bfd59e5f-6767-41f6-8b77-6acec77a0ddc)



![WhatsApp Image 2025-10-11 at 18 50 08_92b80b07](https://github.com/user-attachments/assets/507d05b2-e8bc-4610-9a34-a80dabbc1729)





![WhatsApp Image 2025-10-11 at 18 50 39_fba9ed85](https://github.com/user-attachments/assets/911b1266-b36e-4e16-a51c-5a05026aceaa)



























  


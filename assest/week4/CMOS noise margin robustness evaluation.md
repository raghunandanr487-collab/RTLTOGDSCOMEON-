# 🍋‍🟩NOISE MARGIN

- Noise Margin is the maximum noise voltage that can be tolerated by a logic circuit without causing an error in the output logic level.
-  there are two types of noise margin

# 🔊 noise margin high and noise margin low 
 ## Noise Margin High (NMH):
- The maximum noise voltage that can be added to a logic HIGH input without changing the output logic.

## 🍕 Noise Margin Low (NML):
- The maximum noise voltage that can be added to a logic LOW input without changing the output logic.


### 📈so now we will see the image of the graphs of invertor with labbled vil,voh,vol,vih,vdd

![WhatsApp Image 2025-10-18 at 19 23 35_4652a153](https://github.com/user-attachments/assets/a30a2c7f-12a7-4cd4-bff7-8dc418a61246)

- this is the image in which i have shown the three different graphs in which first one is ideal
  senario.
- second one is more partical senario.
- thrid is the real graph we get.
- In the real graph we can see that now voh is not equal to vdd.


## 📈 we can see  other graphs also 

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/bed9de77-479b-4395-8a12-40c49788905f" />


- Noise margin high=NMH=VOH​−VIH
- Noise margin low=​NML=VIL​−VOL​


## 💹 now we will draw this graph on the stright line 

![WhatsApp Image 2025-10-18 at 19 37 13_fbe3f873](https://github.com/user-attachments/assets/20aea741-1c9e-41fd-9856-fcd8f2574e2e)


- so we can see there is three different region .
- first region = logic high region ,its diff tells that if that much amout of noise will come then it can bear it and give output as logic one .
- second region = it is the undefined region in which output can either oen or zero.
- thrid region = it is the low region and it  diff tells that if that much amout of noise will     come then it can bear it and give output as logic zero .


## 🧙now we will summaries it by looking at the graph 

![WhatsApp Image 2025-10-18 at 19 45 43_a383ccbe](https://github.com/user-attachments/assets/47d2900b-50a6-407f-a90f-98ec9018f8b6)

- so for any signal to be considered as logic zero and logic one ,it should be in the NML and  NMH ranges ,respectively

- these are the bumps which are comming ,and other all the thing we clearly see from the image.
  

 #  💫Static behavior evaluation: Cmos invertor robustness

  ## 🤷now in this we will see how the NMH and NML will changes when we change the width of pmos
   and nmos 

  ### 💹 now we will see the graph of which size nmos and pmos taken 

  <img width="1835" height="984" alt="Screenshot 2025-10-18 154446" src="https://github.com/user-attachments/assets/11679b33-cab9-4ced-a440-bf869ecb0601" />

## 🔭 Observations 
- From the table, the Noise Margins are: NMH​=0.3V,NML​=0.3V
- These values indicate that the inverter can tolerate up to 0.3 V of noise on either the
   logic high or logic-low input without logic error.

- the symmetry of NMH and NML (both =0.3) shows that the inverter is well balanced likely
   because   𝑊p/Lp=Wn/Ln.


## 🎭now we willsee the another image in which we have inc the width of pmos and see what happen 

  <img width="1801" height="1067" alt="Screenshot 2025-10-18 154508" src="https://github.com/user-attachments/assets/40574799-a07d-42b1-9969-2332ab67e783" />

## 🔭obseravtion 
-in this we can see the NMH is  inc becuase we have doublle the width of pmos and we know pmos 
is reponsiable for the logic one 
- for the low logic it is still same .


  ## 💹 now we will see another few more graph also in whcih we will do the tipple ,fouth and fifth width of the pmos and see what will happen

 <img width="1864" height="1043" alt="Screenshot 2025-10-18 154525" src="https://github.com/user-attachments/assets/41029b41-6f6d-4d8c-8672-9ae3c546567e" />


<img width="1837" height="1029" alt="Screenshot 2025-10-18 154541" src="https://github.com/user-attachments/assets/59fe4649-ee24-44a3-8071-816b304b0c4d" />

  <img width="1763" height="1027" alt="Screenshot 2025-10-18 154556" src="https://github.com/user-attachments/assets/f323f3b3-ba2d-4d1e-85d2-48cfbf267466" />


## ⚡observations 

 - now we can see that on increasing only the pmos width we will not get the noise margin high
   it will become the constant after some time and noise margin of low will start decresing
   because  the power of the pmos is start dominating and nmos losses it power to hold the zero

 -  so this thing we can clearly see in the graphs as we inc the width then also the NMH remain same and the NML start deceresing.
      
## 🧭 table 

| Wp/Lp | x.Wn/Ln | NMH  | NML  | Vm    |
| ----- | ------- | ---- | ---- | ----- |
| Wp/Lp | Wn/Ln   | 0.3  | 0.3  | 0.99V |
| Wp/Lp | 2Wn/Ln  | 0.38 | 0.3  | 0.97V |
| Wp/Lp | 3Wn/Ln  | 0.4  | 0.22 | 0.85V |
| Wp/Lp | 4Wn/Ln  | 0.42 | 0.2  | 0.75V |
| Wp/Lp | 5Wn/Ln  | 0.45 | 0.18 | 0.67V |


## ⚡Observations:

- In this table, we can see that there is not much variation of Noise Margin (High and Low) for different values of Vm.

- The value of threshold voltage vm decreases slightly when the ratio of NMOS width to length increases.

- From the above data, we do not need to worry about it if there is a small error in the fabrication process, because you will still get nearly equal NMH and NML values.


#  spice simulation 

## it is the file i have used for the simualtion


<img width="1128" height="1027" alt="Screenshot 2025-10-18 174804" src="https://github.com/user-attachments/assets/f118ea45-7ff1-4e56-a7a2-e80860aa10dd" />




## graph of the simulation


<img width="1739" height="939" alt="Screenshot 2025-10-18 210447" src="https://github.com/user-attachments/assets/2c5dda76-cb7d-4062-b2cd-932d14d87212" />


# results images 

<img width="264" height="38" alt="Screenshot 2025-10-18 180027" src="https://github.com/user-attachments/assets/2dfb3749-a46d-4d3a-8142-72af5a06e5b8" />

<img width="324" height="76" alt="Screenshot 2025-10-18 180945" src="https://github.com/user-attachments/assets/3b8327e6-8cee-469b-a71e-3df21421932c" />

- first one is for VMH= 0.776-1.686
- second one is for VML=0.98-0.104









































  




  

  
  








  
 
















  











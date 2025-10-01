IN This we will look into the synth and simulation mismatch both of the gtkwave will come will be different 

## what is GLS
- running the testbench with netlist as desgin under test
- netlist is logically same as RTL  code

## why GLS

- verify the logical correctness of the desgin after synthesis
- Ensuring the timing desgin is meet
- for this GLS needs to run with delay annotion 



in first image the file name bad_mux is used 


<img width="818" height="763" alt="Image" src="https://github.com/user-attachments/assets/d09ed6a2-b31b-4e82-829b-e956a2e42c05" />




now we will see the simulation gtkwave of bad_mux and this we can this y is only change when the sel will change 
and  if i0 and i1 is changing but if sel is out chnage it will not show the change value it shows 
perviously recorded value only




<img width="819" height="757" alt="Image" src="https://github.com/user-attachments/assets/3a7d218a-8e22-4b38-bb66-af2c004f23f2" />



now if we sysnthsis it then it will come prefect if the input is changhing the then the updated 
values we will get here so







<img width="825" height="751" alt="Image" src="https://github.com/user-attachments/assets/537bcf1f-ec9f-40b3-bbc0-4588083758b8" />


there is the mismatch in the simulation and synthasis !!


NOW WE WILL LOOK AT OTHER EXAMPLE 

the filename blocking_caveat.v 


<img width="823" height="752" alt="Image" src="https://github.com/user-attachments/assets/1a5003f3-ec31-4c9e-bee7-b0ed20014ac3" />



now we will look at the simulation gtkwave of it


<img width="823" height="763" alt="Image" src="https://github.com/user-attachments/assets/98dc6d63-4f81-4759-b312-577e1578ec18" />




after synthasis we go the dot file like 


<img width="819" height="763" alt="Image" src="https://github.com/user-attachments/assets/df632320-811b-4777-8c46-c19b1fe4f8ac" />



now we will the image of the gtkwave after synthasis and writing the netlist file 
and  in this we can clearly see the mismatch between the both the wave of sysnthasis and simulation

<img width="823" height="755" alt="Image" src="https://github.com/user-attachments/assets/da17af4c-2fea-4d20-b127-0dbcab7f0176" />




so conclusion is that on doing the bad coding we get the dufficulties in synthasis and simulation  so always give the else conditon ,it just an example and use the always(*) so it will causes to occurs always block when any of input is changes!! 















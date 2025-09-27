NOW  IN THIS FILE WE WILL LOOK INTO CASE CONDITION AND IF ,ELSE  HOW TO WRITE IT CORRECTLY SO WE GET THE DESIERD OUTPUT 



first image is the verilog file of incomp_if.v

here else consditon is not written so there will be glitches 
<img width="819" height="767" alt="Image" src="https://github.com/user-attachments/assets/2d27cba1-c130-47f9-9ef3-f39f80446fd5" />

now we will see the gtkwave of it 

in this we can see the giltch that there is inferred latch is created 

<img width="814" height="762" alt="Image" src="https://github.com/user-attachments/assets/4fc54b77-4578-4d63-82d5-12a449263e11" />


now we will see the synthasis desgin of it 

in this we can see clearly there is dff which is acting as a latch 

<img width="825" height="766" alt="Image" src="https://github.com/user-attachments/assets/f5ccc3ea-0db0-4e30-b59f-399118820d03" />




now we will the another example of it file name income_if2.v

image of it 


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
in this we can see there is no else is used so it will creat the inffered latch again 
image of it 
<img width="826" height="754" alt="Image" src="https://github.com/user-attachments/assets/2ccf98c9-15dc-4618-9f98-2cf9649522c8" />



Now we will see the gtkwave of it and we can there is an inffered latch is created when i0 and 
i2 both are zero then it will hold the previous vaule 


<img width="830" height="752" alt="Image" src="https://github.com/user-attachments/assets/1edac466-4eab-464a-8148-99210d720852" />



 we get dot file after the synthasis
in this we can see the output behaviour as the or of the i0 and i2 is 1 then only we get y will change otherwise it wil hold the previous value

 <img width="823" height="761" alt="Image" src="https://github.com/user-attachments/assets/2b73bb4a-83e5-4acf-93ce-330ef6e94c3c" />





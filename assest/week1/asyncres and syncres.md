

In this i have learn about the asyncres irrespective of the clock it get Q CHANGES its value

this is the screenshot


<img width="946" height="903" alt="Image" src="https://github.com/user-attachments/assets/9279c2f7-6212-439e-b74f-dd779920c4cc" />


next image is shown is the asyncset without dependence of the clk 


<img width="923" height="923" alt="Image" src="https://github.com/user-attachments/assets/e18beeaa-592c-4ce6-a7cc-6937162cf39a" />



next image is of the syncres which means it will change the value of Q only when the clk at posedge ,irrespetive of the sync_reset

<img width="931" height="892" alt="Image" src="https://github.com/user-attachments/assets/40b2d589-c8e0-4b0f-824a-358570d13e32" />



now I have shown the  dff_asyncres dot file in which it is showing the result after synthesis and there is shown as one inverter because we are reseting the output so ,inverter is there and 
dff is there and there are two cells ,
here is the image of it 


<img width="933" height="892" alt="Image" src="https://github.com/user-attachments/assets/0e93bb8b-817f-4dca-87fd-a9c67bcc74da" />


next one is the syncres dot file which there are two cells  one of the nor and there is dependence on the clk and it also give the simplest version removing unsed signals also 

[image ]

<img width="933" height="918" alt="Image" src="https://github.com/user-attachments/assets/0bfdcd71-e218-4c76-a9bd-9c5fbd9ccff4" />










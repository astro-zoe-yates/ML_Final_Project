# Light Curve Classification Using ML
This project was created for the purpose of the final project of Machine Learning in Geology 6932 for Spring 2025. This code uses a convolusional neural network to detect and classify signals in Transitting Exoplanet Survey Satelite (TESS) light curves (LC) and provide best fit parameters using MCMC technique. 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
I. INTRODUCTION
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Inputs:
  - TIC ID of object of interest
  - Period in days of object of interest

Outputs:
  - Likelihood of each type of signal present in the light curve
  - MCMC best-fit-parameters for the transit

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Package Dependencies:
  - Numpy
  - Matplotlib
  - Pandas
  - Lightkurve
  - SKLearn
  - Tensor Flow
  - Batman

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

II. Data 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The NN is initially trained using TESS observations of 3 classes: 
  1. Planetary Signal (Olmschenk et. al 2021)
  2. Binary Signal (Michael)
  3. No Indetifiable Signal (need to find)

This list of ojects used were taken from previous works using TESS data. The stellar TIC IDs and parameters are found in their individual text files uploaded here. 

The TESS LC observations are found using the LightKurve (LK) search function, which finds each observation from TESS of that object from each sector it was osberved. We found the best sector of TESS observations for each object by _____, normalized the flux and phase folded the light curve using lcf.fold over the period to find an easily identifiable signal. Below shows the difference before and after the transformation using LK.


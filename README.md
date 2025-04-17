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
Some discussion about why this project is important 

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Training Data 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The NN is initially trained using TESS observations of 2 classes: 
  1. Planetary Signal (Olmschenk et. al 2021)
  2. Binary Signal (Michael)

This list of ojects used were taken from previous works using TESS data. The stellar TIC IDs and parameters are found in their individual text files uploaded here. In order to avoid class imbalances, we used 175 objects for each class.  

The TESS LC observations are found using the LightKurve (LK) search function, which finds each observation from TESS of that object from each sector it was osberved. We found the best sector of TESS observations for each object by a signal-to-noise threshold, normalized the flux, and phase folded the light curve using lcf.fold over the period to find an easily identifiable signal. The observations were cleaned for outlier data points and noisy observations, and were adjusted using a masking routine to clean up data around the signal. Below shows an example of a planetary signal and binary signal post cleaning: 


![pl_curve_0](https://github.com/user-attachments/assets/5df38d15-860d-4035-bfaf-05ad848f50b2)

Figure 1: TESS Light curve for TIC ID 7548817 with known planetary signal after data cleaning processing

![eb_curve_116](https://github.com/user-attachments/assets/dec3f821-001f-492c-a57e-6fabadf69593)

Figure 2: TESS Light curve for TIC ID 372909935 with known binary signal after data cleaning processing

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Neural Network
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

In order to train the NN, we used the images of the plotted light curves for each class. We used a 2D Convolusional Neural Network, optimized to handle image files for training. The NN contains 5 layers with the final 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Algorithm Accuracy
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. MCMC Fit for Planetary Signals
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Running the Code
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Conclusions
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

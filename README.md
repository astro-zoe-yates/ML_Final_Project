# Light Curve Classification Using ML
This project was created for the purpose of the final project of Machine Learning in Geology 6932 for Spring 2025. This code uses a convolusional neural network to detect and classify signals in Transitting Exoplanet Survey Satelite (TESS) light curves (LC) and provide best fit parameters using MCMC technique. 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
I. INTRODUCTION
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Inputs:
  - TIC ID of object of interest
  - Period in days of object of interest

Outputs:
  - Classification of object's TESS Light Curve and the likelihood 
  - MCMC best-fit-parameters (planet transits only)

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
Project Summary: 

For this project, we proposed to use a Convolusional Neural Network (CNN) to identify and classify signals4 in stellar light curves taken by the Transiting Exoplanet Survey Satellite (TESS). Investigating unique signals in the light curve observations of stars is crucially important to key objectives within the field including the discovering Earth-like planets and developing our understanding of planetary systems like our own. Using Machinal Learning (ML) techniques to classify signals in our observations presents an efficient mechanism to finding exciting targets of interest for future observations, as well as provides context to how ML can be implemented into astronomical research. With this work, we will attempt to forge a new technique of analyzing light curves and calculate parameters of their respective1y planetary systems.

Light curves are plots describing the flux or brightness of a star over a continuous period of time. They are popularly used to look for objects that would cause a star’s brightness to fluctuate including planet transits, binary star transits, stellar activity, and variable stars. Transits occur when an object, a companion star or transiting planet, passes in front of a star, causing a decrease in overall brightness. Figure 1 below shows an example of the shape of the two types of light curves: planetary signal and binary signal, however with noisy or unclean data, it can be difficult to identify and classify these signals, thus we employ a NN to aid in the classification of these signals. 

<img width="583" alt="Screenshot 2025-04-17 at 12 32 14 PM" src="https://github.com/user-attachments/assets/d29da604-6e22-4dc2-b683-678fdc8cb27d" />

Figure 1: TESS Light Curves with a model fit of the confirmed exoplanet TOI 150.1 (top panel), and the eclipsing binary system TOI 276 (bottom panel)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Training Data and Data Availability 
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The NN is initially trained using TESS observations of 2 classes: 
  1. Planetary Signal (Olmschenk et. al 2021)
  2. Binary Signal (Prša et al. 2022)

This list of ojects used were taken from previous works using TESS data. The stellar TIC IDs and parameters are found in their individual txt or csv files uploaded here. In order to avoid class imbalances, we used 175 objects for each class.  

The TESS LC observations are found using the LightKurve (LK) search function, which finds each observation from TESS of that object from each sector it was osberved. We found the best sector of TESS observations for each object by a signal-to-noise threshold, normalized the flux, and phase folded the light curve using lcf.fold over the period to find an easily identifiable signal. The observations were cleaned for outlier data points and noisy observations, and were adjusted using a masking routine to clean up data around the signal. Figures 1 and 2 shows examples of a planetary signal and binary signal post cleaning. 

![pl_curve_0](https://github.com/user-attachments/assets/5df38d15-860d-4035-bfaf-05ad848f50b2)

Figure 2: TESS Light curve for TIC ID 7548817 with known planetary signal after data cleaning processing

![eb_curve_116](https://github.com/user-attachments/assets/dec3f821-001f-492c-a57e-6fabadf69593)

Figure 3: TESS Light curve for TIC ID 372909935 with known binary signal after data cleaning processing

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Convolusional Neural Network and Accuracy
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

In order to train the model, we used the images of the plotted light curves for each class. We used a 2D Convolusional Neural Network (CNN), optimized to handle image files for training to attempt to classify LC signals into the two classes: eclipsing binaries and planets.  Our CNN contains three 2D convolusional layers and then two fully connected layers after flattening the images, passing through 26 epochs for accuracy convergence. We use the ReLu activation functions with a final output activation function of SoftMax due to our binary classification. The model is evaluated based on the accuracy of seperate validation data, to understand the performance of the CNN, and a confusion matrix was produced to examine how the model performed for each class. Figures 4 and 5 show the accuracy curve and the confusion matrix for the CNN. 

![image](https://github.com/user-attachments/assets/e255a035-bdba-4d47-b410-ba1f8c720f3d)

Figure 4: Accuracy curve for both the training and validation data over each epoch 

![image](https://github.com/user-attachments/assets/a7971100-2892-4d7a-af8c-e9ea43439798)

Figure 5: Confusion matrix for the CNN, displaying the performance accuracy of each class

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
III. MCMC Fit for Planetary Signals
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

For the planet transit signals that have been classified by the 2D CNN, a secondary notebook was made to fit a planet transit model (BATMAN) to the data using an MCMC (emcee). The output parameters give you the planets radius (in units of stellar radii), the semi-major axis of the orbit (in units of stellar radii), and the point of mid transit, all with uncertainties. The code outputs an image of the flux and model fit (Figure 6) as well as a corner plot of the MCMC run (Figure 7).

![image](https://github.com/user-attachments/assets/44836987-26d3-4fbd-9bf0-345689bb0bc4)

Figure 6: MCMC Fit of planet transit light curve

![image](https://github.com/user-attachments/assets/7b4e1a10-5156-476b-a8df-9eefa7990273)

Figure 7: Corner plot of MCMC fitting

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
II. Running the Code
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

The code is split up into two notebooks:
  1. CNN_signal_classification.ipynb
  2. Planet_MCMC.ipynb

Due to the numpy version dependencies, these two tasks cannot be put into the same notebook. 

The first notebook will run the CNN using either the data from the txt files provided on this GitHub Repository, or with the option of uploading your own training image files. The last cell in the notebook allows the user to input a TIC ID and it's orbital period in days. Once run, the code will retreive the TESS observations using LK, sigma clip them for noise reduction and contamination, and classify the image using the CNN model. The code will output a phase folded light curve plot, as well as the classification and confidence from the model. It will also save the TIC ID, period, time array, and flux array into a new txt file called 'object_paraneters.txt', to allow for easy integration into the MCMC notebook. If the classification is 'planet signal', the code will prompt you to upload the txt file to the MCMC notebook for further star/planet parameter calculation using BATMAN and MCMC fitting. 



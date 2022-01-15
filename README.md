# BootCamp-Mod-19-Neural_Network_Charity_Analysis
Performing analysis use neural networks to determine which organizations are best for donating to and which are too high risk.


## Overview of Project

### Purpose
The purpose of this analysis is to use neural networks to help Becks, a data analyst for Alphabet Soup, a non-profit foundation that supports other charitable organizations, determine which organizations are best for Alphabet Soup to donate to.


## Analysis and Results
### Preprocessing
- Charity data was provided by Alphabet Soup.
- The data contained many columns with non-numeric data that needed to be preprocessed before being able to use the data in the neural network.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Initial_Unique_Values.png"width="527" height="228"/></p>

- Also, many of these columns contained data that had more than 10 unique values. Therefore, unique counts were determined along with density plots to bin the lower frequency values into another category of other for both the APPLICATION_TYPE and CLASSIFICATION columns.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/intial_app_counts.png"width="410" height="231"/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/reduced_app_counts.png"width="533" height="421"/></p>


<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/initial_class_counts.png"width="421" height="180"/>&nbsp;&nbsp;&nbsp;<img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Reduced_class_counts.png"width="533" height="418"/></p>


- With all categorical data narrowed down to 10 unique values, OneHotEncoder was used to convert the categorical data to numerical data and merged with the previously already numerical data.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Cat_counts.png"width="657" height="168"/></p>

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Merge_table.png"width="620" height="222.5"/></p>

- The variables were then split up into targets and features.
  * The target column is IS_SUCCESSFUL.
  * The feature columns are STATUS, ASK_AMT, and all of the numerical data created by the OneHotEncoder function.
  * The variables that are neither targets nor features are EIN, NAME, and all the original categorical columns.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/variables.png"width="691" height="120"/></p>

### Compiling, Training, and Evaluating the Model
- After creating the variables, the data is split into training and testing data.
- Then, the data was scaled to avoid large value from biasing the data.
- The neural network model was then created.
  * The number of input features was 44.
  * 2 hidden layers were created to have a low number of layers for computational reasons but still allowing for a deep learning model.
  * The first hidden layer has 80 neurons, since that is about twice as many as the input features.
  * The second hidden layer has 30 neurons, since this is less than half of first hidden layer and the goal is to keep the computation load light if possible.
  * The outer layer has 1 neuron.
  * This all creates 5,981 parameters.
  * Both hidden layers used the relu function because this seems to be a complex model and it is better at handling more complex models.
  * The outer layer used the sigmoid activation function because we are classifying the donations either as risky or not risky.
- The model was compiled.
- The model was fit with 100 epochs and with checkpoint saving every 5 epochs.
- The model was then evaluated using the testing model.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/model.png"width="610" height="385"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/run_model.png"width="669" height="328"/></p>

### Model Performance
- The model was only 72.5 % successful, therefore not achieving the target model performance of 75%.
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Test_results.png"width="659" height="112"/></p>


### Increased Performance
- Many steps were taken to try to increase the model's performance
* First, adding more hidden layers. First, 3 layers, then 4, then 5, then at 6 layers the model performed worse than originally.
* Second, tried to reduce the number of columns in the table, specifically thinking that the ASK_AMT column had too many unique values, even though they were numeric, was causing noise in the model.
* Third, changing the number of neurons in the model to more or less depending on the number of epochs the model got a little better, but not enough to change the testing performance.
* Finally, changing the activation function. The only change that ultimately made a different was changing the hidden layers activation functions from relu to elu. When this change was made, the model went to 100% which is not very realistic.

<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Opt_Model.png"width="710" height="405"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Opt_model_fit.png"width="787" height="515"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-19-Neural_Network_Charity_Analysis/blob/main/Graphics/Opt_model_test.png"width="666" height="106"/></p>

## Summary
- With the data provided, the best performance from the model was 72.5%.
- After many changes to try to improve the model, the only thing that would seem to add in improving the model would be to get more data. Either, more rows of data, or new columns of data for the same organizations are needed, since it seems that there is an aspect of the classification that is not accounted for with the data provided.

# SOMNI
Sleep data imputation package

This is the algorithm package to handle missing data problems in sleep diary. Link to the paper:


[Please cite as]


### How to use
There are 2 algorithms here, which are using individual data (individual_model) to train the model, or use a global model (global_model) trained from multiple patients to handle the missing data.

Code:
There are 2 main py files, individual_model_handle and global_modle_handle, which will contain the functions to handle the missing data.<br />
There are 2 folders, data, which to contain all the datasets, and necessary data functions handler. The folder models contain the NMF handlers, the model's structures, and training supporting functions.

Data requirements:
The file provided should have following criteria:
- Columns should contain SleepStatus, actigraphy columns (which can include missing data)
- Data are measured minute-wise/per minute

System requirements:
- numpy, pandas, torch, and surprise package for NMF

<br />

#### 1. Individual_model
We first propose the individual model, which can process the sleep diary singly without additional data. The file contains this algorithm is individual_model, with the function named individual_model_handle. 

 How to use:
- Put the file needed to handle into the directory data (same position as the synthetic_data.csv)
- In a py/ipynb file, import the function: from individual_model import individual_model_handle
- individual_model_handle requires 3 arguments: filename, which should be the name of the file needed for handling, the mode should be either handle or evaluate. Handle will simply output a file, with all the missing labels have been filled, thanks to the model trained on the nonmissing data. Evaluate will mask some data of the file into missing, which will be used to test for the algorithm. Finally, param_choice will decide the parameters of the gamma distributions, which will generate the maskings for the algorithm. 2 options are tune or default, with default uses our parameters learnt from our datasets, while tune will estimate the parameters from the input filename, based on methods of moments

#### 2. global_model

 How to use:
 - Put the file needed to handle into the directory data (same position as the synthetic_data.csv)
 - In a py/ipynb file, import the function: from global_model import global_model_handle
 - global_model_handle requires 3 arguments: filename, which should be the name of the file needed for handling, the mode should be either handle or evaluate. Handle will simply output a file, with all the missing labels have been filled, with our default global_model. 
 Evaluate will mask some data of the file into missing, and train a new model, with starting point being our model, and fine-tune using the data from the targeted dataset and the missing masks. Finally, param_choice will decide the parameters of the gamma distributions, which will generate the maskings for the algorithm. 2 options are tune or default, with default uses our parameters learnt from our datasets, while tune will estimate the parameters from the input filename, based on methods of moments

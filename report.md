# Neural Network Model Report

## Overview

Data sourced online containing multiple variables and a target variable of successful venture was used to model, train, and fit a deep learning model using tensorflow. The model was tuned using `keras_tuner` to automate the optimization process. The highest accuracy score yielded by the tuner was approximately 73.36%.

## Results

### Preprocessing

The csv file used contained the following variables/types:

#### ID

* `EIN` – Identification
* `NAME` – Identification

#### Features

* `AFFILIATION` – Affiliated sector of industry
* `CLASSIFICATION` – Government organization classification
* `USE_CASE` – Use case for funding
* `ORGANIZATION` – Organization type
* `STATUS` – Active status
* `INCOME_AMT` – Income classification
* `SPECIAL_CONSIDERATIONS` – Special considerations for application
* `ASK_AMT` – Funding amount requested

#### Target

* `IS_SUCCESSFUL` – Was the money used effectively


#### The data was preprocessed in 3 steps:

1. `EIN` and `NAME` were dropped as they are not features, only identification

2. `APPLICATION_TYPE` binned less frequent observations into an `other` category

    * Same with `CLASSIFICATION`
    
3. Categorical columns were coded with dummy variables

Then the preprocessed dataset was split into training and testing sets.

### Model

Tensorflow was used to comple, train, and evaluate a model.

#### Initial model

The initial model created had The below parameters:

    Model: "sequential"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     dense (Dense)               (None, 84)                3612      
                                                                     
     dense_1 (Dense)             (None, 20)                1700      
                                                                     
     dense_2 (Dense)             (None, 1)                 21        
                                                                     
    =================================================================
    Total params: 5,333
    Trainable params: 5,333
    Non-trainable params: 0
    _________________________________________________________________
    
        * The first layer contains 84 neurons in pursuit of a rule of thumb regarding having twice as many neurons as features (of which there are 42)
        
        * Activation functions are respectively the following: relu, sigmoid, sigmoid
        
    * This model was unable to reach target performance, capping out with an accuracy of 72.991% and a loss of 55.52%
    
#### Optimization

Using `keras_tuner`, the optimization process was automated. Below are the hyperparameters and accuracy metrics for the top three:

Model 1:

Loss: 0.552553117275238, Accuracy: 0.7336443066596985
Hyperparameters:
{'activation': 'relu',
 'first_units': 23,
 'num_layers': 2,
 'tuner/bracket': 2,
 'tuner/epochs': 20,
 'tuner/initial_epoch': 7,
 'tuner/round': 2,
 'tuner/trial_id': '0043',
 'units_0': 26,
 'units_1': 6,
 'units_2': 21,
 'units_3': 26,
 'units_4': 6}
-----------------------------------------

Model 2:

Loss: 0.5548089742660522, Accuracy: 0.7335277199745178
Hyperparameters:
{'activation': 'relu',
 'first_units': 19,
 'num_layers': 3,
 'tuner/bracket': 0,
 'tuner/epochs': 20,
 'tuner/initial_epoch': 0,
 'tuner/round': 0,
 'units_0': 6,
 'units_1': 21,
 'units_2': 1,
 'units_3': 16,
 'units_4': 21}
-----------------------------------------

Model 3:

Loss: 0.5533367991447449, Accuracy: 0.7334110736846924
Hyperparameters:
{'activation': 'tanh',
 'first_units': 21,
 'num_layers': 5,
 'tuner/bracket': 1,
 'tuner/epochs': 20,
 'tuner/initial_epoch': 7,
 'tuner/round': 1,
 'tuner/trial_id': '0080',
 'units_0': 11,
 'units_1': 26,
 'units_2': 6,
 'units_3': 11,
 'units_4': 21}
-----------------------------------------

Model 1 was exported as an optimized version

## Summary

The optimization approach could not yield an accuracy score of 75%; other attempts yielded less than the current top model score of 73.36%. The loss is also notable with it being 0.55.

Perhaps a dataset with more variables is needed. Other machine learning models could be used too, or a linear regression model which is often used for classification.

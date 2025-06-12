# IQ-prediction

## Data
Download models and data from this link https://www.dropbox.com/scl/fo/p1htyqwjn2dacnyqo9e3n/AERcKtoMJaRSdQNdEQ-Ref4?rlkey=k54r04xtpaynoygu61uijzoqo&st=ldz5g7zz&dl=0.
Models should be placed into `Models/` directory.
Data should be placed into `data/` directory.

## Example
Example of usage can be seen in the "Gradient boosting model time evaluation" section of the notebook.

## Explanation
I'm using pandas library to read the data for training from `data/data_AMP_PCS_reduced.csv`.
For training the model I use the train/test split to get the train data for the model and then to validate it using data unseen previously in the test dataset. [wiki](https://en.wikipedia.org/wiki/Training,_validation,_and_test_data_sets).
First, I've used the Random forest model as a baseline for training, but the experiments showed that Gradient boosting model performed better in our problem. So we can ignore the Random forest part.
For testing the performance of the model, I've used such metrics as MSE, MAE, RMSE and R2 score, which are standard metrics for regression models.
The training process is done once using `regr_Q.fit(X_train, y_train.iloc[:,1])` call and the weights for the trained models were saved to dropbox. I have trained models for I and Q values separately so to use the model for prediction of I, `gradient-boosting-I-1.pkl` weights should be loaded.
For using the model in production we first need to load the model using `regr_I = pickle.load(open("Models/gradient-boosting-I-1.pkl", "rb"))`.
Then, to predict the values of I, the data should be prepared the same way as the test dataset was formed. It should have same dimensions and same order of features to work properly.
The original dataset was prepared using the [link](https://github.com/AnnaBobrikova/ComptonSlabTables/blob/main/MKMS.py) code so it can be reaused to create the production data for actually running the model on the new data. 

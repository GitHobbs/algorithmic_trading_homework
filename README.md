# algorithmic_trading_homework
Creating and backtesting an algorithmic trading strategy using machine learning

# Baseline Performance

The baseline scenario resulted in the following Classification Report (based on the testing data) as well as the below graph showing actual returns vs strategy returns.

precision    recall  f1-score   support

        -1.0       0.43      0.04      0.07      1804
         1.0       0.56      0.96      0.71      2288

    accuracy                           0.55      4092
   macro avg       0.49      0.50      0.39      4092
weighted avg       0.50      0.55      0.43      4092


![Actual Returns vs Strategy Returns](plot_1.png)

## Baseline Conclusions

Beginning in 2019, the strategy returns outpaced the actual returns in nearly every instance.  The model was able to predict buy signals with relatively good accuracy, however it was not able to predict sell signals very well (.04 recall).


# Step 1: Tune the training algorithm by adjusting the size of the training dataset

In this instance, I doubled the size of the training data by changing the DateOffset parameter to 6 months.  This resulted in the following  Classification Report and returns plot:

precision    recall  f1-score   support

        -1.0       0.44      0.02      0.04      1732
         1.0       0.56      0.98      0.71      2211

    accuracy                           0.56      3943
   macro avg       0.50      0.50      0.38      3943
weighted avg       0.51      0.56      0.42      3943

![Actual Returns vs Strategy Returns](plot_2.png)

## Step 1 Conculsions

Increasing the training data window did not help the accuracy of the model, nor did it improve the strategy returns.  In fact, it hurt in both cases.  Recall on the sell classification was cut in half from it's previously low level and strategy returns were outperformed by actual returns from late 2018 to early 2020.

# Step 2: Tune the trading algorithm by adjusting the SMA input features

In this instance, I increased the size of both the long and short SMA windows by a factor of 2.5 (short window - 10, long window - 250)

precision    recall  f1-score   support

        -1.0       0.42      0.13      0.20      1544
         1.0       0.56      0.86      0.68      2006

    accuracy                           0.54      3550
   macro avg       0.49      0.50      0.44      3550
weighted avg       0.50      0.54      0.47      3550

![Actual Returns vs Strategy Returns](plot_3.png)

## Step 2 Conclusions

Increasing the SMA windows greatly helped the recall on the sell signals.  However, it was outperformed by actual returns across the board.

# Step 3: Choose the set of parameters that best improved the trading algorithm returns.

Neither adjustment improved algorithm returns.

# Evaluate a New Machine Learning Classifier

For this instance, I used a Decision Tree Classifier instead of an SVM.  

precision    recall  f1-score   support

        -1.0       0.43      0.98      0.60      1484
         1.0       0.45      0.01      0.02      1921

    accuracy                           0.43      3405
   macro avg       0.44      0.50      0.31      3405
weighted avg       0.45      0.43      0.27      3405

![Actual Returns vs Strategy Returns](plot_4.png)

## New Classifier:  Conclusion

Well, using a Decision Tree instead of a Support Vector Model reversed the recall issues I was having earlier.  It was able to accurately predict a lot of sell signals, but not buy signals.  It made a lot of -1.0 guesses, so this makes sense.  Meanwhile, the returns on this model were drastically lower than actual returns.  Therefore, I was not able to imporove on the original model with any of my adjustments in this assignment.

# Machine-Failure-prediction

Univariate Analysis 
The air temperature distribution looks slightly left skewed with a mean temperature around 300K.
There is no outlier present.
"The process temperature distribution looks slightly left skewed with a mean temperature around 329K.
There is no outlier present."
The rotational speed is right skewed with many outliers on the upper quartile.
Some of the manufacturing operations are performed at a higher speed.
Tool wear is uniformly distributed with some of the higher values being less frequent.
Around 60% of products are of low quality, 30% are of medium quality whereas 10% are of high quality
In 96.6% of observations the machine does not fail while in 3.4% of observations it fails.

Bi-variate Analysis
There's a positive correlation between the air temperature and process temperature.
There's a negative correlation between the rotational speed and torque.
No other variables are correlated
Machining of high-quality products is less prone to failure.
Most of the failures of the manufacturing system occur at higher Process temperature.
There is a clear boundary showing separation of failure status based of the values of Rotational speed.
Manufacturing system is more prone to failure at lower Rotational speed than at higher rotational speed.

Data Preprocessing
We had seen that around 96.6% of observations belongs to class 0 (Not Failed) and 3.37% observations belongs to class 1 (Failed), and this is preserved in the train and test sets

Model Evaluation Criteria 
Predicting a machine will not fail but in reality, the machine will fail (FN)
Predicting a machine will fail but in reality, the machine will not fail (FP)
If we predict that a machine will not fail but in reality, the machine fails, then the company will have to bear the cost of repair/replacement and also face equipment downtime losses
If we predict that a machine will fail but in reality, the machine does not fail, then the company will have to bear the cost of inspection
The inspection cost is generally less compared to the repair/replacement cost
The company would want the recall to be maximized, greater the recall score higher are the chances of minimizing the False Negatives.

Decision Tree Class Weights
Model is able to perfectly classify all the data points on the training set.
0 errors on the training set, each sample has been classified correctly.
As we know a decision tree will continue to grow and classify each data point correctly if no restrictions are applied as the trees will learn all the patterns in the training set.
This generally leads to overfitting of the model as Decision Tree will perform well on the training set but will fail to replicate the performance on the test set.
There is a huge disparity in performance of model on training set and test set, which suggests that the model is overfiiting.

PRE PRUNING
Hyperparameter tuning is crucial because it directly affects the performance of a model.
Unlike model parameters which are learned during training, hyperparameters need to be set before training.
Effective hyperparameter tuning helps in improving the performance and robustness of the model.
The below custom loop for hyperparameter tuning iterates over predefined parameter values to identify the best model based on the metric of choice (recall score).
The model is giving a generalized result now since the recall scores on both the train and test data are coming to be around 0.97 which shows that the model is able to generalize well on unseen data.

General Review when machine will fail at what combinations
Based on this decision tree data, we can expect the machine to fail under several conditions:

High rotational speed (> 1379.50 RPM) combined with high tool wear (> 202.50).
High rotational speed with low torque (≤ 15.45).
High rotational speed, moderate tool wear (> 202.50 but ≤ 219.50), and high UDI (> 3529.00).
Lower rotational speed (≤ 1379.50 RPM) but very high tool wear (> 206.50).
Lower rotational speed with high torque (> 52.85) and high tool wear (> 185.50).
Lower rotational speed, high air temperature (> 301.55), and specific UDI ranges.

The most significant factors appear to be rotational speed, tool wear, torque, and UDI (Unscheduled Downtime Indicator).

Decision Tree (Post pruning)


Cost complexity pruning provides another option to control the size of a tree.
In DecisionTreeClassifier, this pruning technique is parameterized by the cost complexity parameter, ccp_alpha.
Greater values of ccp_alpha increase the number of nodes pruned.
Here we only show the effect of ccp_alpha on regularizing the trees and how to choose the optimal ccp_alpha value.
In the post-pruned tree also, the model is giving a generalized result since the recall scores on both the train and test data are coming to be around 0.96 which shows that the model is able to generalize well on unseen data.
Rotational speed and Torque are the most important features for the post pruned tree
Decision tree models with post-pruning is giving high recall scores on both training and test sets.
Therefore, we are choosing the post-pruned tree as our best model.

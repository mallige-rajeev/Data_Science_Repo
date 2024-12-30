What is HAR?

Human Activity Recognition (HAR) involves classifying human actions using data from sensors.
Applications: Fitness tracking, healthcare monitoring, and smart devices.

Objective:

Develop a machine learning model to accurately classify human activities, such as "standing" and "walking," using accelerometer and gyroscope data. This involves data preprocessing, model evaluation, and optimization for robust, 
real-time performance on mobile devices, even with noisy or limited data.

Problem Statement:

Human Activity Recognition (HAR) plays a vital role in areas like healthcare, sports analytics, and mobile applications by enabling the detection of human movements in real time. 
This project focuses on leveraging data from Inertial Measurement Unit (IMU) sensors, specifically accelerometers and gyroscopes in mobile devices, to accurately classify fundamental human activities. The goal is to distinguish between "standing" and "walking," using machine learning techniques to create a robust and deployable solution for real-time activity monitoring and analysis.

Dataset Overview:

Dataset Size: 31,991 entries with 8 features.

Sensors Used:

1. Accelerometer: Measures linear motion.
2. Gyroscope: Measures angular motion.

Features:
1. Sensor Data: accX, accY, accZ, gyroX, gyroY, gyroZ.
2. timestamp
3. Target: Activity

Initial Observations:
Accelerometer features exhibit higher variability for certain activities.
Gyroscope features complement accelerometer data but show broader overlap.

Data Cleaning:

Handled duplicate rows.
Addressed outliers to reduce noise.
Applied StandardScaler to ensure zero mean and unit variance.
Visualized feature distributions to identify overlaps and patterns.
To address class imbalance, the Synthetic Minority Oversampling Technique (SMOTE) was applied, which generates synthetic samples for the minority class, ensuring a balanced distribution of activity labels and improving model training stability.

Key Observations:

Accelerometer Features (accX, accY, accZ):
They exhibit clearer separations between standing and walking. accZ appears particularly strong for distinguishing activities due to the sharp difference in stability versus variation.

Gyroscope Features (gyroX, gyroY, gyroZ):
These show broader overlaps between the two activities, likely reflecting less variation in angular motion between standing and walking. 
 
Among all features, accelerometer data (accX, accY) shows higher variability compared to the gyroscope data. This indicates that the accelerometer is capturing more fluctuation in movement, which could be crucial for differentiating between "standing" and "walking."

A combination of accelerometer and gyroscope features will likely yield the best classification results.

Modeling Approach:

1. Preprocessed data with StandardScaler.
2. Used machine learning algorithms like
	a. Logistic Regression: Simple and interpretable model
	b. Support Vector Machine: Ensures that a robust margin-based classifier is tested for performance comparison
	c. K Nearest Neighbor: A good non-parametric model.
	d. Random Forest: Robust ensemble model.
	e. Gradient Boosting: Enhanced predictive accuracy.
			XGBoost
			CatBoost
3. Hyperparameter optimization via cross-validation
4. Regularization
5. Manual Tuning to get better results

Modeling Insights:

1. Random Forest Classifier gave the highest test accuracy (96.5%), followed by XGBoost (96.04%) and CatBoost (95.78%).
2. Logistic Regression achieved the highest AUC-ROC score (0.84), followed by SVC (0.8321), CatBoost (0.8059) and XGBoost (0.8042). These models have better discrimination ability to distinguish between the classes (standing vs. walking).
3. XGBoost and CatBoost both performed well in terms of AUC-ROC, which indicates their ability to correctly differentiate between classes. They also performed well on the other metrics, especially in Test Accuracy, and XGBoost provided the best balance of precision, recall, and F1 score.
4. Overfitting was majorly seen in models like Logistic Regression, Support Vector and KNNeighbors. CatBoost, XGBoost and Random Forest did not experience major overfitting issues and could be reduced with hyperparameter tuning. Hence, XGBoost and CatBoost were chosen for hyperparameter tuning.

Tuning and Regularization:

1. Hyperparameter tuning increased test accuracy by a small margin but didn't help increase AUC score. Hence, I went forward with regularization of both these models.
2. After Regularization, we observe that  there is a drop in AUC-ROC compared to that before tuning these models and it suggests that the model's ability to discriminate between classes (standing vs walking) may have reduced slightly as a trade-off for reduced overfitting.
3. We also observe that with better test accuracy and AUC-ROC, XGBoost takes the upper hand among the models. Upon manually tuning XGBoost, we were able to reduce overfitting to a great extent while maintaining a good AUC-ROC score.
4. The XGBoost model demonstrates excellent performance during cross-validation, with a high mean ROC-AUC score of 0.9943 and a low standard deviation of 0.0008, indicating consistent and reliable classification across the folds. This suggests the model is well-suited for distinguishing between the target classes with minimal variability.

Key Insights:

1. True Positives (Walking classified correctly): The model correctly identified 9019 instances of the "Walking" class, which shows strong performance in identifying this dominant class.
2. False Negatives (Walking misclassified as Standing): There are 370 instances where "Walking" was misclassified as "Standing" .
3. The imbalance in the dataset is reflected in the higher True Positive (TP) rate for "Walking."

Conclusion:

This project aimed to classify human activities as 'Standing' or 'Walking' using accelerometer and gyroscope data, a critical task for applications in health monitoring, sports analysis, and mobile computing. Several machine learning models, including Logistic Regression, SVC, KNN, Random Forest, XGBoost, and CatBoost, were developed and rigorously evaluated to identify the most effective approach.

After extensive experimentation, the XGBoost model emerged as the optimal choice, achieving a test set accuracy of 95.62% and an AUC-ROC score of 0.8348, indicating robust overall performance and improved generalization with reduced overfitting. Despite its strong results, the analysis revealed a challenge in detecting the minority class ('Standing') due to class imbalance, highlighting an area for potential improvement.

In conclusion, this project demonstrates the feasibility of using sensor data for accurate human activity recognition and lays the groundwork for real-time applications and further enhancements through advanced balancing techniques or feature engineering.
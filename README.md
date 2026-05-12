# Machine Learning Model for Abnormal Heartbeats in ECG datasets
For our 4th year capstone project, we wanted to develop a long-term, real-time ECG monitor for detecting early signs of heart arrhythmia. Current testing and analysis of patient ECG data is retroactive and time-consuming. After the ECG collects about a week's worth of data, the patient will bring the data to the cardiologist, where they will have to sort through hundreds of thousands of individual heart beats to find abnormalities. To assist cardiologists and patients, we trained an ML model (random forest), using data from the MIT-BIH heart arrhythmia dataset, to detect abnormal heartbeats in real-time. This way, abnormalities can be detected as soon as they occur. The goal was to reach a detection accuracy of 80%.

## What We Learned During Development
In order for our model to digest the ECG data, the data was split based on the RR interval of the heartbeat. Each beat is associated with a label (from the database), and were assigned either a 0 (normal) or 1 (abnormal). Then, the dataset made up of 48 patients was split into three categories: training, validation, and test.
During preprocessing, we created many variables for the model to learn from. The image below shows the feature importance of the model.
 
<img width="664" height="455" alt="image" src="https://github.com/user-attachments/assets/f3268bab-a3a0-4749-a7ad-517461466f36" />
 
Initially, the data was unbalanced since there were more normal heartbeats than abnormal beats in every patient. A solution to this was by bootstrapping the minority group. The image below shows the number of data points for each type of heartbeat.
 
<img width="218" height="162" alt="image" src="https://github.com/user-attachments/assets/c96a5e69-a5b1-4340-8883-93967f60627d" />


The image below is an example of the model making predictions on one of the datasets from the test group.
 
<img width="1012" height="393" alt="image" src="https://github.com/user-attachments/assets/2b69b9e6-cb26-4774-929a-a4efba42b6f0" />

In the end, the highest prediction the model could come to was around 77% accuracy. However, after doing further research, accuracy is not fit for determining the performance of a model for abnormal heart detection. Using the classification_report function from sklearn.metrics, the following results were found.
 
<img width="423" height="142" alt="image" src="https://github.com/user-attachments/assets/d9737e20-8a28-423d-a1f8-adefe885afaa" />
 
Unlike accuracy, these metrics show how well the model is learning both kinds of heartbeats. The precision, similar to accuracy, is a measure of how many heartbeats were actually abnormal, recall is a measure of how many abnormal heartbeats were correctly identified, and f1-score is a balance between the two.
Although the data was balanced using bootstrapping during preprocessing, the model still learned from the normal beats better than the abnormal beats. In medical applications, it is better for the model to produce false positives rather than miss any abnormal beats, which is why optimizing the recall metric is the most important.

## Future Direction
In the future, we have found that the best model to use for heart arrhythmia detection are CNNs, as many researchers have been moving forward with this method. Additionally, using recall and f1-score for evaluating the model is a necessity for future development.

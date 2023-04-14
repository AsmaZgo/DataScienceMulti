# **System Design Exercice**

## Problem definition:
For an anomaly detection use case, we wish to design a platform (i) for near real-time data ingestion from a data stream and (ii) for model training (online and batch) to solve the problem. The online (re)training should be executed at the rate of data arrival, and the batch (re)training should be triggered at the end of the day, integrating new data into the existing model. 

## Model selection for the anomaly detection problem:
The model that should be used for this problem is a decision tree called isolation trees. Outlier data is easier to detect in the tree. Additionally, an anomaly score can be used to detect data points that are located far away from the other data points.

## Architecture design for the model training (online and batch)
High-level project setup:

- Streaming engine that supports near real-time events like Apache Spark Streaming.
- Distributed machine learning techniques to be able to handle all the incoming batch data at the end of the day, like Spark ML or deep learning. The incoming data frequency is 10 MB per second, which will create a voluminous amount of data to process by the end of the day.
- Spark Dataframe API can be used to access the batch training data at the end of each day.
- Jupyter Notebook and Python can be used for development.

The final project should be composed of the following components:

- Stream data access layer
- Batch data access layer
- Model training and evaluation layer
- Feature selection and engineering layer
- Model adapting layer


![image](https://user-images.githubusercontent.com/10657080/232062716-1ba60d68-9988-4fe0-824c-241ac19e5dd2.png)


According to the architecture, the online training method that we chose is model retraining. In order to update the model, we need to update the hyperparameters. For example, we should use lower values for learning rates to avoid retraining the model and instead only update the existing model with the new data. In this case, the new and old data should be combined to create a train and test set.

One approach to integrating online learning and offline model updates is to continuously update the model with each new data arrival. In this case, the learning rate should be updated at every new type of retrain, and this hyperparameter should be studied at the proof of concept (POC) step accordingly. Another approach would be to store all updates in one data store and retrain the model only once a day.

In order to offer near-real-time visualizations (live dashboards) for model monitoring and prediction, we propose using a streaming engine such as Apache Spark Streaming or Apache Flink to collect the streams. Spark streams produce micro-batches, and Spark Streaming offers this functionality with a streaming delay of just 1 second.

For the dashboard, we propose using Jupyter Notebook and designing it with libraries such as Seaborn or using the Dash library in Python.

The implementation needed for the given scenarios is as follows:

- Summary statistics of the data stream: Use aggregation methods in the streaming engine.
- Anomaly scores: Extract anomaly scores by interrogating the stored model.
- Other metrics and KPIs can be computed on the fly while learning anomalies and streaming data, and collected in an insight database (key-value store to ensure very fast data access).

The final architecture becomes when we add the dashboard :


![image](https://user-images.githubusercontent.com/10657080/232062601-d0cb5b42-f8b1-4417-a40d-87896fa47deb.png)

# **System Design Exercice**

## Problem definition:
For a anomaly detection use case we wish to design the platform for the near real time data ingestion from a data stream and for the model training (online and batch) to solve the problem. The online (re)training should be executed at the rate of the data arrival and the batch (re)training should be triggered at the end of the day integrating new data to the existing model. 

## Model selection for the anomaly detection problem:
The model that should be used for this problem is a decision tree called: isolation trees. The outlier data is easier to be detected in the tree.
Also, an anomaly score can be used to detect data points that are located far away from the other data points.

## Architecture design for the model training (online and batch)
High level project setup : 
- use streaming engine that support near real time event like Apache Spark Streaming
- use distributed machine learning technique to be able to support all the incoming batch data at the end of the day like spark ml or deep learning. The incoming data’s frequency is 10 mb per second which will create by the end of the day a voluminous amount of data to process
- spark dataframe api can be used to access the batch training data in the end of each day
- use python to develop in spark ml or tensorflow (deep learning)
- you can use Jupiter note book for the developing or another big data notebook library: apache ziplin
 the final project should be composed of the following components: 
	- stream data access layer 
	- batch data access layer
	- model training and evaluation layer
	- feature selection and engineering layer
	- model adapting layer
	- batch access layer
  

![image](https://user-images.githubusercontent.com/10657080/232062716-1ba60d68-9988-4fe0-824c-241ac19e5dd2.png)


According to the architecture the online training model that we chose is model retraining.
In order to update the model, we need to update the hyper parameters and use for example lower values for learning rates in order to avoid retraining of the model and only updating the existing model with the new data. In this case new and old data should be combined and from their combination a train and test sets are created.
One approach to integrate online learning and offline model update is to keep updating the model at each new data arrival (the learning rate in this case should be updated at every new type of retrain and this hyper parameter should be studied at the poc step accordingly). Another approach would be to store all the updates in one data store and retrain only once a day.

In order to offer near real time visualizations (live dashboards) for model monitoring and for prediction we propose to use a streaming engine like apache spark streaming or apache flink to collect the streams. Spark streams produces micro batches. spark streaming offers this functionality and the streaming delay is in this engine: 1 second.
We propose for the dashboard using Jupiter notebook and designing it with libraries in jupyter notebook like seaborn or using dash library in python.

The implementation needed for the given scenarios:
- summary statistics of the data stream: use aggregation methods in the stream engine
- anomaly scores: extract anomaly scores from interrogating the stored model 
- other metrics and kpis can be computed on the fly while learning anomalies and streaming data and collected in an insight database (key value to ensure very fast data access) 

The final architecture becomes when we add the dashboard :


![image](https://user-images.githubusercontent.com/10657080/232062601-d0cb5b42-f8b1-4417-a40d-87896fa47deb.png)

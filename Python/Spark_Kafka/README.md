# Kafka-Spark-MongoDB

Background :
  StopFire is a campaign to predict and stop the fire in Victorian cities. They have employed sensors in different cities of Victoria and have collected a large amount of data. 

We will use part of the data from this campaign to:
1. Design a NoSQL database and store the data
2. Design an application for streaming and processing the data

The data sheets we will use are:
- hotspot_historic.csv  
- climate_historic.csv 
      **These two for database creating**

- hotspot_AQUA_streaming.csv 
- hotspot_TERRA_streaming.csv 
- climate_streaming.csv
      **These three for data streaming**

The programming language and tools we will use are:
- Python  
- MongoDB
- Apache Kafka
- Apache Spark


>* Task A: Created MongoDB Database

Please see **Database_Creation.ipynb**



>* Task B: processing Data Streams:

In this task, we will implement multiple Apache Kafka producers to simulate the real-time streaming of the data which will be processed by Apache Spark Streaming client and then inserted into MongoDB. 
The overall system architecture is shown in the figure below. 

```
                             |-----------------------------------------------------------------------------------------|
Event/Data Streaming         |    | Data Stream Processing | Data and Result Storage| Data and Result Distribution     |
___________                  |    |                        |                        |                                  |
Producer 1 |-------------|   |    |                        |                        |                                  |
-----------              |   |    |                        |                        |                                  |                |   |    |                        |                        |                                  |
___________             _______   |        _______         |      ___________       |                                  |
Producer 2 |---------->| Kafka |--|-------| Spark |--------|------| Mongo DB |------|-------------->Visualisation/<----|     
-----------            ---------  |       ---------        |      ------------      |                 Front End
                         ^        |                        |                        |
___________              |        |                        |                        |
Producer 3 |-------------|        |                        |                        |
-----------                       |                        |                        |

```

- **Kafka_Producer.ipynb** for three producers
- **Spark_Streaming_Application.ipynb** for Data stream processing
- **Data_Visualisation.ipynb** for visualisation



**Note: If Github fails to load the notebook, please download it and use Jupyter Notebook to run the file.**
 
 
 

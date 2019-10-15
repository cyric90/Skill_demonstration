# Kafka-Spark-MongoDB

Background :
  StopFire is a campaign to predict and stop the fire in Victorian cities. They have employed sensors in different cities of Victoria and have collected a large amount of data.
  They have hired us as the data analyst to migrate their data to the NoSQL database (MongoDB). They want us to analyse their data and provide them with results.
  In addition, they want us to build an application, a complete setup from streaming to storing and analyzing the data for them using Apache Kafka,  Apache Spark Streaming and MongoDB.  

We will use part of the data from this campaign to:
1. Design a NoSQL database and store the data.
2. Design an application for streaming and processing the data

The data sheets we will use are:
○ hotspot_historic.csv  
○ climate_historic.csv 
**These two for database creating

○ hotspot_AQUA_streaming.csv 
○ hotspot_TERRA_streaming.csv 
○ climate_streaming.csv
**These three for data streaming

The programming language and tools we will use are:
○ Python  
○ MongoDB
○ Apache Kafka
○ Apache Spark

Task A: Created Mongo DB Reference Data model

I had to use 2 data set to decide on to the data model, which are: 
>* hotspot_historic.csv (2668 rows)
>* climate_historic.csv (366 rows)

After Exploring through the data set it can be noticed that: 
>- Dates are unique in climate data. 
>- Datasets can be mapped through date column in both the datasets. 
>- Cardinality of the dataset is 1 to N.
>- Datasets cardinality justify either of "one to few" or "one to many" relation where on an average one row of climate data gets mapped to 10 rows of hotspot data (in this case there are ~100 rows with no data mapped to historic which further increase the count of mapping).
>- If the relation is "one to few" we use Embedded nodel and if the relationship is "one to many" we prefer reference model (Less than 1000),

It is a little ambigous situation where both the model will work fine. For Instance, If Embeded model is used perfomance of the query will be better as it will not have to query separate collection. But in this instance the primary focus of the task is to investigate on fire incidents and there might be a possibility that we might need to query the hotspot data which might make it  hard to access the details as stand-alone entities.

Therefore, in this case, we have decided to use the **reference model**. It will also ensure that searching and fetching of independent entities can be done easily and quickly. To make the referencing simple we will introduce an integer object id which will act as reference to the _id of the hotspot data. 

We have also incorporated **two way referencing** to reference from hotspot data to climate data to cater to the possible need of identifying a fire to particular sensor.

To enhance the perfomance of our model we have also incorporated **Denormalization** of "surface_temperature_celcius" and "confidence" from historic data to climate data under the assumption that it is analysis task and there will high read to write ratio and no Update will be required to the dataset.(which is one of the major disadvantage of denormalization). 




```



Task C processing Data Streams:
In this task, we will implement multiple Apache Kafka producers to simulate the real-time streaming of the data which will be processed by Apache Spark Streaming client and then inserted into MongoDB. 
The overall system architecture you will be developing is shown in the figure below. 
```

Event/Data Streaming              | Data Stream Processing | Data and Result Storage| Data and Result Distribution
___________                       |                        |                        |
Producer 1 |-------------|        |                        |                        |
-----------              |        |                        |                        |
                         v        |                        |                        |
___________             _______   |        _______         |      ___________       |
Producer 2 |---------->| Kafka |--|-------| Spark |--------|------| Mongo DB |------|-------------->Visualisation/
-----------             --------  |       ---------        |      ------------      |                 Front End
                         ^        |                        |                        |
___________              |        |                        |                        |
Producer 3 |-------------|        |                        |                        |
-----------                       |                        |                        |

```

1. Simulating real-time data using Apache Kafka Producers.   
  >- a. Event Producer 1: Program that loads all the data from climate_streaming.csv and randomly feed the data to the stream every 5 seconds in Assignment_TaskC_Producer1.ipynb. 
  >- b. Event Producer 2: Program that loads all the data from hotspot_AQUA_streaming.csv and randomly feed the data to the stream every 10 - 30 seconds in Assignment_TaskC_Producer2.ipynb. 
     AQUA is the satellite from NASA that reports latitude, longitude, confidence and surface temperature of a location.  
  >- c. Event Producer 3: Program that loads all the data from hotspot_TERRA_streaming.csv and randomly feed the data to the stream every 10 - 30 seconds in Assignment_TaskC_Producer3.ipynb. 
     TERRA is another satellite from NASA that reports latitude, longitude, confidence and surface temperature of a location. 
 
 
 2. Stream Processing using Apache Spark Streaming.  
    >- Streaming Application: Write a streaming application in Apache Spark Streaming which has a local streaming context with two execution threads and a batch interval of 10 seconds. 
       The streaming application will receive streaming data from all three producers. 
       
 3. Data Visualisation using MatPlotLib  
    >- a. Streaming data visualization: For the incoming climate data plot the line graph of air temperature against arrival time with some interesting points such as maximum and minimum values.
    >- b. Static data visualization: 
    
      >-   i. Bar chart showing Records with the top 10 number of fires.
         
       >-  ii. Fire locations in the map with air temperature, surface temperature, relative humidity and confidence (Merging two streams).
 
 
 

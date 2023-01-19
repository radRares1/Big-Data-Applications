# Big Data Car Traffic Monitor

## Problem.

![Alt text](https://github.com/radRares1/Big-Data-Applications/blob/main/goal.PNG )

The problem that this project tries to solve is to monitor the traffic data in the capital cities of Romania’s counties. This monitor is regarding the volume of cars and the decibels levels in the busiest streets in each city using Business Intelligence dashboards.
Since this is only a POC, for convenience, we are generating synthetic data. After careful consideration we decided to use the Databricks Labs Data which allows the custom creation of data with base values, different distributions, datetime data, these being both in streaming and batch format.

## Storage.

To store the data, we chose two types of solutions for our data. First being the S3 storage of the AWS Cloud provider, used for the historical data. The second is the Databricks File System storage provided by the Databricks platform, this one is used to hold the streaming data, which later is stored as historical data also. Additionally, we are using Delta tables for each of our pipeline stages (bronze, silver, gold).

## Formats.

As for formats, we are using parquet for the historical data from S3 and delta for the streaming and historical data stored on DBFS. Delta allows us to store the data as Delta Tables which allow for versioning of the data, checkpointing for the streams and ACID transactions logging, which are great advantages over the classical parquet.

## Data Sources and Design.

![Alt text](https://github.com/radRares1/Big-Data-Applications/blob/main/archi.PNG )

Since we have two data sources, we have two pipelines, but the process is the same:  We start the stream generator, we read the stream and write it also as a stream in the bronze table, we read the bronze table in streaming format to maintain the continuity of the pipeline, we clean the invalid data and write the stream into the silver table sink, next we read a new stream from the silver table, augment it with geospatial data about the cities and write the stream to the golden table.


## Results.

As for the BI [dashboard](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/2996911928916293/752184719582461/1386756242519882/latest.html), we create map visualization with hourly aggregates of the number of cars, run plots with the increase or decrease in car numbers, car type, brands, colors distributions and comparisons between historical and real time read data.
For the technical part, we chose Spark and Spark Structured Streaming for the manipulation of data and used Python as the programming language. Databricks for the notebook storage and creation, data holding, table storage, spark cluster hosting and library installation. AWS for the storage which was accessible with credential security in Databricks. The Delta Lake was also a core technology which allowed us to use the data both as streaming and batch.


 

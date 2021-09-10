---
title: "Databricks Delta Spark Cache"
date: 2020-05-12T12:14:34+06:00
image: "images/blog/terraform-databricks-labs/featured-image.png"
tags: ["Azure", "Databricks"]
description: "Databricks Delta Cache and Spark Cache"

draft: false
---

As data sizes and demand increases as time goes on, you often see slowness on Databricks this can be due to number of factors from security, network transfers, read/write requests, and memory space.  

A common cause of this is when Databricks has to contently reads parquet files from the file system, increasing the I/O and network throughput. Databricks has to manage and monitor the cluster to ensure it does not exceed the I/O treads threshold and that the workers have enough memory to cope with the jobs being executed.  

To handle the constant data transfer and I/O treads, you can cache data on to Databricks clusters. There are two types of caching available on Databricks, Spark and Delta caching.  

In this post I will explain the key differences and benefits of Spark and Delta cache. 

### Spark Cache

Spark cache stores and persists data in-memory blocks or on local SSD drives when data does not fit in-memory. It is available on all clusters as it is the out of the box option, basically the native Spark option. The contents of a dataframe or RDD are cached in an uncompressed format. 

Spark cache must be implicitly called using the `.cache()` command against the dataframe that is being cached, meaning it becomes a lazy cache operation which is compiled and executed later. 

### Delta Cache

Delta cache in the other hand, stores the data on disk creating accelerated data reads. Copies of the files are stored on the local nodes’ storage and data is automatically cached when files are obtained from a remote location/filesystem using a fast intermediate format. 

This improves query performance as data sits closer to the workers and storing on the local disk frees up memory for other Spark operations. Even though it is stored on disk it is still efficient as it uses a decompression algorithm to retrieve the data fast. 

Delta cache automatically maintains the file consistency and detects any changes to the underlying data files and manages its cache. 

##### Delta Cache Accelerated

Delta cache can be optimised further by using a **`Delta Cache Accelerated`** worker types (i.e. Standard_L series), when configuring the cluster. Delta cache is enabled by default on these worker types and the SSDs are preconfigured to use Delta cache effectively. 

Delta cache does not need to explicitly call as it will automatically caches the data when it is first executed. However, it is useful to call the `CACHE SELECT` command in advance to get consistent query performance. 

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-worker-types.png" alt="adb-cache-worker-types" width="200" align="center">}} <br><br>

## Caching Examples

To demonstrate both Delta and Spark Cache, we can cache some data and compare the outputs metrics using the Spark UI Storage tab.  The Spark UI allows us to monitor the volume of data being cached, read and written.  

For the following code snippets, use a Delta table that has been created using the NYC Taxi trip data from databricks-dataset.  

### Spark Cache Example

First, let’s get a baseline view before caching any dataframe, so execute a `count` query against the Delta table.  

```python

    preCache = spark.sql("SELECT count(*) FROM tripdata")
    display(preCache)

    Command took 13.55 seconds

```

Using the Spark UI Storage tab, you will see that nothing has been cached or read. <br>
*Sometime there may be a small amount data read by the external filesystem but in this case there was none.*

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-spark-storage-ui-pre.png" alt="adb-cache-spark-storage-ui-pre" width="700" align="center">}} <br><br>

Now, execute a `count` query against the Delta table inside a dataframe using `.cache()` and call an action so it executes the command. 

```python

    postCache = spark.sql("SELECT count(*) FROM tripdata")
    postCache = postCache.cache()
    display(postCache)

    Command took 1.30 seconds

```

This time you will see in the Spark UI Storage tab, that it has forced the data behind the DataFrame to be persisted in its RDD form and cached in memory.  

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-spark-storage-ui-post.png" alt="adb-cache-spark-storage-ui-post" width="700" align="center">}} <br><br>
 
### Delta Cache Example

Now, run similar queries on a Delta Cache Accelerated cluster (Standard_L series). 

Once again, let’s get a baseline view before caching, so execute a `count` query against the Delta table.  

```sql

    %sql
    SELECT count(*) 
    FROM  tripdata

    Command took 15.46 seconds

```

Using the Spark UI Storage tab, you can see again that nothing has been cached or read. <br>
*Sometime there may be a small amount data read by the external filesystem but in this case there was none.*

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-delta-storage-ui-pre.png" alt="adb-cache-delta-storage-ui-pre" width="700" align="center">}} <br><br>

Now, cache the Delta table using the `CACHE SELECT` command and re-execute the `count` query against the Delta table. 

```sql

    %sql
    CACHE 
    SELECT * FROM tripdata;

    Command took 7.48 seconds

```

```sql

    %sql
    SELECT count(*) FROM tripdata

    Command took 0.54 seconds

```

This time in the Spark UI Storage tab, you can see that the data has been cached on each node and the volume of data being read and written from IO cache.  

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-delta-storage-ui-post.png" alt="adb-cache-delta-storage-ui-post" width="700" align="center">}} <br><br>
 
## Execution Times

We can compare the execution timings using the Spark UI Jobs tab.  

The Spark cache jobs shows the `postCache` dataframe was executed much faster than the `preCache` dataframe.  

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-spark-jobs-ui.png" alt="adb-cache-spark-jobs-ui" width="700" align="center">}} <br><br>

The Delta cache jobs shows once again that the `post` query was executed faster than `pre cached` query and faster than Spark cache too.  

{{<img src="/images/portfolio/databricks-delta-spark-cache/adb-cache-delta-jobs-ui.png" alt="adb-cache-delta-jobs-ui" width="700" align="center">}} <br><br>

## Summary

Delta cache stores data on disk and Spark cache in-memory, therefore you pay for more disk space rather than storage. 

Data stored in Delta cache is much faster to read and operate than Spark cache. Delta Cache is [10x faster](https://databricks.com/blog/2018/01/09/databricks-cache-boosts-apache-spark-performance.html) than disk, the cluster can be costly but the saving made by having the cluster active for less time makes up for the cluster cost. 

Delta and Spark caching can be used together but can slow the performance down. As Delta cache retrieves the data fasts and performs calculations quickly, so by adding Spark caching it has to retrieve data several times from the SSDs of the original dataframe rather than parquet files slowing the performance down.  

Thanks for reading, I hope you found this post useful and helpful. 

Example notebooks can be found on **[GitHub](https://github.com/FalekMiah01/Azure-Platform/tree/main/Databricks/Delta-Spark-Cache)**. 


<br/><br/>


## **References**

https://docs.microsoft.com/en-us/azure/databricks/delta/optimizations/delta-cache

https://databricks.com/blog/2018/01/09/databricks-cache-boosts-apache-spark-performance.html


---
title: "Databricks Delta Spark Cache"
date: 2020-05-12T12:14:34+06:00
image: "images/blog/terraform-databricks-labs/featured-image.png"
tags: ["Terraform", "Databricks", "Azure"]
description: "This is meta description."
draft: false
---

As data sizes and demand increases as time goes on, you often see slowness on Databricks this can be due to number of factors from security, network transfers, read/write requests, and memory space.  

A common cause of this is when Databricks has to contently reads parquet files from the file system, increasing the I/O and network throughput. Databricks has to manage and monitor the cluster to ensure it does not exceed the I/O treads threshold and that the workers have enough memory to cope with the jobs being executed.  

To handle the constant data transfer and I/O treads, you can cache data on to Databricks clusters. There are two types of caching available on Databricks, Spark and Delta caching.  

In this post I will explain the key differences and benefits of Spark and Delta cache. 

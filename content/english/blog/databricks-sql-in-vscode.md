---
title: "Databricks SQL in VSCode"
date: 2023-01-25T18:00:00+01:00
description : "Using Databricks SQL in VSCode"
type: blog
image: images/portfolio/databricks-sql-in-vscode/dbx-sql-in-vscode-featured.png
author: Falek Miah
tags: ["Azure", "Databricks", "Databricks SQL", "VSCode"]
draft: false
---

Recently, I had the opportunity to explore the Databricks SQL extension for VSCode, and I was thoroughly impressed. 

In December 2022, Databricks launched the [**`Databricks Driver for SQLTools`**](https://marketplace.visualstudio.com/items?itemName=databricks.sqltools-databricks-driver) extension, and although it is still in preview, the features are already good and useful.

For data analysts, report developers and data engineers, having the ability to execute SQL queries against Databricks workspace objects is crucial for streamlining workflows and making data analysis activities much more efficient and quicker. The Databricks SQL extension for VSCode provides just that, with a simple and intuitive interface, this extension makes it easy to connect to Databricks workspace and run SQL queries directly from VSCode.

## Getting Started

First you need to install the [**`Databricks Driver for SQLTools`**](https://marketplace.visualstudio.com/items?itemName=databricks.sqltools-databricks-driver) extension, which is available in the Visual Studio Marketplace.  Then set up the Databricks connection to your workspace using the Databricks Host, Path, and PAT Token.  The following blog by [**`Ganesh Chandrasekaran`**](https://ganeshchandrasekaran.com/run-your-databricks-sql-queries-from-vscode-9c70c5d4903c) will give you the required steps to get started. 

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-01-connections.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-01-connections.png" alt="dbx-sql-01-connections" width="300" align="center"></a> <br><br>

Once you have the extension and connected to Databricks workspace, you can start querying your Databricks workspace using SQL directly from VSCode.

## Features 

Some of the features, I liked…

#### Viewing Objects
You have the ability to view all Databases, Tables, Views and Fields that are in the Databricks workspace, under the **`CONNECTIONS`** panel (left-hand).  This is similar to SQL Management Studio or Azure Data Studio, making it easy to use for those that are familiar with SQL databases.  

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-02-viewing-objects.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-02-viewing-objects.png" alt="dbx-sql-02-viewing-objects" width="300" align="center"></a> <br><br>

#### Viewing Multiple Databases

All the Databases in the Databricks workspace is shown, therefore you can query and view multiple databases in one application.  The `SQL Editor` in Databricks SQL workspace, only allows you to view a single database at a time, therefore when working with multiple databases you must switch between them. 

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-03-multiple-database.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-03-multiple-database.png" alt="dbx-sql-03-multiple-database" width="700" align="center"></a> <br><br>

#### Generate Options
You can generate table records, metadata and insert statements, without having to write any code using the `right-click` option.  

By `right` clicking the table you can select `Show Records`, `Describe Table`, `Generate Insert Query` or using the `Plus` and `Magnifying Glass` icons.

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-04-generate-options.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-04-generate-options.png" alt="dbx-sql-04-generate-options" width="400" align="center"></a> <br><br>

The **`Show Records`** option - selects 50 records from the table. 

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-05-show-records.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-05-show-records.png" alt="dbx-sql-05-show-records" width="700" align="center"></a> <br><br>

The **`Describe Table`** option - show the table metadata information, including the column name and type. 

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-06-describe-table.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-06-describe-table.png" alt="dbx-sql-06-describe-table" width="700" align="center"></a> <br><br>

The **`Generate Insert Query`** option - generates an insert statement for adding data into tables quickly.   

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-07-generate-insert-query.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-07-generate-insert-query.png" alt="dbx-sql-07-generate-insert-query" width="700" align="center"></a> <br><br>

And finally, the **`Add Name(s) to Cursor`** option - allows you to add the table or fields names to the script.

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-08-name-cursor.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-08-name-cursor.png" alt="dbx-sql-08-name-cursor" width="700" align="center"></a> <br><br>

#### Query Results

When you run a SQL query, the results are displayed in a new tab.  Each time a query is executed a new tab is opened, meaning the previous execution results is still available which can be beneficial when debugging queries.

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-09-results-panel.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-09-results-panel.png" alt="dbx-sql-09-results-panel" width="700" align="center"></a> <br><br>

If you’re like me and prefer the result being displayed at the bottom, then you can drag the result tab to the bottom or use the `Split Editor` option. 

#### IntelliSense

It supports intellisense, so real-time suggestions and prompts are given which makes writing the queries much quicker and easier.  This helps eliminate syntax errors, saving time and effort in writing queries and enhances overall productivity. 

<a  href="/images/portfolio/databricks-sql-in-vscode/dbx-sql-10-intelliSense.png" target="_blank">
<img src="/images/portfolio/databricks-sql-in-vscode/dbx-sql-10-intelliSense.png" alt="dbx-sql-10-intelliSense" width="700" align="center"></a> <br><br>

## Summary

Overall, running Databricks SQL queries in VSCode allows you to streamline data analysis processes and make it more efficient. 

With its user-friendly interface, robust features, and seamless integration with Databricks, this extension is the ideal solution for querying your Databricks Lakehouse outside of the Databricks ecosystem.

The extension is a great choice for data analysts and report developers, as it gives them access to the Databricks workspace without the need for direct access, which opens up new opportunities for collaboration and faster insights.

The similarity to other SQL query editors makes this extension a great choice for those who are already familiar with SQL databases, this familiar interface makes it easy to get started and saves valuable time when working with Databricks Lakehouse.

The [**`Databricks Driver for SQLTools`**](https://marketplace.visualstudio.com/items?itemName=databricks.sqltools-databricks-driver) extension is a good tool for anyone working with data in Databricks Lakehouse.  I’m sure there will be more exciting features to come in the future, so it's definitely worth keeping an eye on it.  

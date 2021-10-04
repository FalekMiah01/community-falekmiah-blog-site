---
title: "Connect Databricks to Power BI"
date: 2018-07-15T00:00:00+01:00
description : "Connect Azure Databricks to Power BI without Premium Sku Cluster"
type: blog
image: /images/portfolio/wordpress-blogs/adb-pbi-featured.png
author: Falek Miah
tags: ["Azure", "Databricks", "Power BI"]
draft: false
---

Recently when I tried to connect Azure Databricks to Power BI Desktop using the preview Spark (Beta) connector and I experienced some problems where I did not have a Premium Sku Cluster.

In this blog I will give a brief description of how to connect Azure Databricks using Power BI Desktop without having the a Premium Sku Cluster.

<h3>How to Connect</h3>

Connecting Azure Databricks to Power BI Desktop using the Spark (Beta) connector is quite simple and can be done in a few steps.

<ul>
 	<li>Start an Azure Databricks <strong>Cluster</strong> that has tables.</li>
 	<li>Create non-expiring <strong>Access Token</strong> in Azure Databricks, under <strong>User Settings</strong>.</li>
 	<li>Open <strong>Power BI Desktop</strong>, select <strong>Get Data</strong> and choose <strong>Spark (Beta) </strong></li>
 	<li>Enter <strong>Server URL</strong>, select <strong>Protocol</strong> and <strong>Data Connectivity</strong></li>
 	<li>Select the tables you need for <strong>report or analysis</strong>.</li>
</ul>
<em>For more information, I recommend you read <a href="http://blogs.adatis.co.uk/plamenamincheva/post/Power-BI-with-Azure-Databricks-for-Dummies-(in-15-minutes)">Power-BI-with-Azure-Databricks-for-Dummies</a> blog.</em>

<br><br>
<h3>**Where’s the problem?**</h3>

Locating the Server URL details can be a bit complicated than you would expect.  The Server URL is constructed using the JDBC URL information, which can normally be found under the JDBC/ODBC tab in the Clusters settings.

However, if you do not have a Premium SKU cluster it will be greyed out and not available, as the JDBC/ODBC connectivity option is only available if you have a Premium SKU cluster.

{{<img src="/images/portfolio/wordpress-blogs/adb-pbi-jdbc-tabs.png" alt="adb-pbi-jdbc-tabs" width="700" align="center">}} <br><br>

<br><br>
<h3>How to resolve this?</h3>

If you don’t want to change to Premium SKU but still want to connect to Power BI, you can do this by obtaining the JDBC URL information from the URL bar of the Cluster configuration page.

{{<img src="/images/portfolio/wordpress-blogs/adb-pbi-jdbc-url.png" alt="adb-pbi-jdbc-url" width="700" align="center">}} <br><br>

It does mean you will need to do the following additional steps to get the values in the right places to construct the final Server URL.

<ol>
 	<li>Take the first part of the <strong>URL</strong> (Region URL) up to the forward slash.  i.e.<span style="color: #3366ff;"> <em>https://westeurope.azuredatabricks.net</em></span></li>
 	<li>Add a <strong>colon</strong> and <strong>port number</strong> (443) with a forward slash at the end.  i.e. <em><span style="color: #999999;">https://westeurope.azuredatabricks.net<span style="color: #3366ff;"><strong>:443/</strong></span></span></em></li>
 	<li>Add the <strong>SQL Protocol</strong> (sql/protocolv1) with a forward slash at the end.   i.e. <em><span style="color: #999999;">https://westeurope.azuredatabricks.net:443/</span><strong><span style="color: #3366ff;">sql/protocolv1/</span></strong></em></li>
 	<li>Add <strong>o/</strong> and then copy the <strong>O</strong> value from the <strong>URL</strong> including a forward slash at the end.   i.e. <span style="color: #999999;">https://westeurope.azuredatabricks.net:443/sql/protocolv1/</span><span style="color: #3366ff;"><strong>o/1659108793111072/</strong></span></li>
 	<li>Lastly, take the <strong>Cluster Id</strong> value from the <strong>URL</strong> and add to the end.   i.e. <em><span style="color: #999999;">https://westeurope.azuredatabricks.net:443/sql/protocolv1/o/1659108793111072/</span><span style="color: #3366ff;"><strong>0517-135903-outdo75</strong></span></em></li>
</ol>

Now you have constructed the final Server URL, you can enter this into the Power BI Spark (Beta) dialog box.  Example of the final Server URL address:

<em><span style="color: #3366ff;">https://westeurope.azuredatabricks.net:443/sql/protocolv1/o/1659108793111072/0517-135903-outdo75</span></em>

You must select the <strong>HTTP</strong> under <strong>Protocol</strong> and either <strong>Data Connectivity</strong> mode.  Once the <strong>Access Token</strong> credentials have been entered in the next dialog box, you will be able to select the required tables for report or analysis.

<br><br>
<h3>Wrap up</h3>

I hope you found this workaround useful, hopefully soon Azure Databricks will provide the Server details without having to constructed it yourself.

<br><br>
---
title: "An Ultimate Guide to Databricks Unity Catalog"
date: 2024-02-06T18:00:00+01:00
description : "An Ultimate Guide to Databricks Unity Catalog"
type: blog
image: images/portfolio/databricks-unity-ultimate-guide/dbx-unity-introduction-featured.png
author: Falek Miah
tags: ["Azure", "Databricks", "Databricks Unity Catalog"]
draft: false
---

Databricks Unity Catalog (UC) has gained significant attention lately, with Databricks making huge investments and shifting to make it the default choice for all new Databricks accounts.  

<br>

## What is Databricks Unity Catalog?

Unity Catalog is Databricks’ governance solution and serves as a unified system for managing data assets. 

It acts as a central storage repository for all metadata assets, accompanied by tools for governing data, access control, auditing, and lineage. 

Unity Catalog streamlines the security and governance of the data by providing a central place to administer and audit data access. It maintains an extensive audit log of actions performed on data across all Databricks workspaces and has effective data discovery capabilities. 

Essentially, it brings all your Databricks workspaces together, offering fine-grained management of data assets and access. This not only streamlines operations by reducing maintenance overheads but also accelerates processes, increases efficiency and productivity. 

<br>

## Why Databricks Unity Catalog?

Databricks gained popularity for introducing the Lakehouse architecture, establishing a resilient platform for data storage and processing. 

The Lakehouse concept relies on the Delta file format as its driving force, effectively tackling data management challenges within Lakehouse platforms. However, there remained gaps in data discovery and governance, as well as a lack of fine-grained security controls within these Lakehouse data platforms.

Databricks introduced Unity Catalog to bridge these gaps and to eliminate the need for external catalogs and governance tools. Crucially, Databricks is making these capabilities available by default as part of its platform – potentially offering a huge win for customers who adopt Unity Catalog. 

<br>

## Key Features of Databricks Unity Catalog

The key features of Databricks Unity Catalog revolve around data discovery, governance, access, lineage, and auditing. Let's explore these features:

### Data Discovery

Unity Catalog offers a structured way to manage metadata, with enhanced search capabilities while ensuring security is based on user permissions. It allows tagging and documenting data assets, offers a comprehensive search interface, and utilises lineage metadata to represent relationships within the data. 

Users can explore data objects in Unity Catalog through Catalog Explorer, based on their permission levels. They can use languages like SQL and Python to query and create datasets, models, and dashboards from the available data objects. Users can also check field details, read comments, and preview sample data, along with reviewing the full history and lineage of the objects.

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-01-data-discovery.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-01-data-discovery.png" alt="Data Discovery – Catalog Explorer" width="800" align="center"></a>

*Data Discovery – Catalog Explorer*

<br><br>

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-02-data-discovery-search.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-02-data-discovery-search.png" alt="Data Discovery – Search Capabilities" width="800" align="center"></a>

*Data Discovery – Search Capabilities* 

<br>

### Data Governance

Unity Catalog acts as a central repository for various data assets, such as files, tables, views, volumes, etc. It incorporates a data governance framework and maintains an audit log of actions performed on data stored within a Databricks account. 

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-03-data-governance.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-03-data-governance.png" alt="Data Governance – Grant Privileges" width="400" align="center"></a>

*Data Governance – Grant Privileges*

<br>

### Data Access

Unity Catalog provides a centralized platform to manage data access policies that are applied across all relevant workspaces and data assets. 

The access control mechanisms use identity federation, allowing Databricks users to be service principals, individual users, or groups. In addition, SQL-based syntax or the Databricks UI can be used to manage and control access, based on tables, rows, and columns, with the attribute level controls coming soon. 

Fine-grained privileges operate across various levels of the metastore's three-level namespace, with inheritance occurring downward in the namespace hierarchy. 

You can control who can access things like clusters, DLT pipelines, SQL warehouses, and notebooks at the workspace level using Access Control Lists (ACLs). Admin users and users with ACL management privileges can manage these ACLs.

Through Unity Catalog's access control management, you enhance security by eliminating direct access to the underlying data storage, therefore adding an additional layer of protection.

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-04-data-access.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-04-data-access.png" alt="Data Access – Permissions and Grants" width="800" align="center"></a>

*Data Access – Permissions and Grants*

<br><br>

### Data Lineage

Unity Catalog has end-to-end data lineages for all workloads, giving visibility into how data flows and is consumed. Data lineage has become vital in understanding data movement, tracking, monitoring jobs, debugging failures and tracing transformation rules. 

The lineage feature provides a comprehensive view of both upstream and downstream dependencies, including the data type of each field. Users can easily follow the data flow through different stages, gaining insights into the relationships between tables and fields.

The lineage tracks the individual fields within a dataset, and not just at the table level. This enables users to examine the transformations applied at the field level and understand the components of the field sources. This makes the feature extremely valuable and effective.

As data lineage holds critical information about the data flow, it uses the same governance and security model to restrict access based on users' privileges. 

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-05-lineage.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-05-lineage.png" alt="Data Lineage" width="800" align="center"></a>

*Data Lineage* 

<br><br>

### Data Auditing

Unity Catalog automatically captures user-level audit logs and records the data access activities. These logs encompass a wide range of events associated with the catalog, such as creating, deleting, and altering various components within the metastore, including the metastore itself. Additionally, they cover actions related to storing and retrieving credentials, managing access control lists, handling data-sharing requests, and more.

The built-in system tables let you easily access and query the account's operational data, including audit logs, billable usage details, and lineage information. 

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-06-system-tables.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-06-system-tables.png" alt="Data Auditing - System Tables" width="550" align="center"></a>

*Data Auditing - System Tables* 

<br>

## Key Components of Databricks Unity Catalog

### Unity Catalog Architecture

Unity Catalog has a metastore, similar to Hive metastores, but this layer of abstraction allows more efficient and improved categorization of data assets. The metastore serves as the primary container for objects in Unity Catalog, holding crucial information about data assets such as tables, databases, and other data objects, making it easier to manage and discover data. The metadata contains essential information such as schema definitions, data types, data source locations, and the permissions governing access to these data assets. 

There is a well-defined and efficient upgrade path designed for migrating from Hive metastore to the Unity Catalog metastore, simplifying the adoption of Unity Catalog. This streamlined process ensures a smooth migration, minimising disruptions, and maximising the benefits of Unity Catalog features immediately.

Unity Catalog is restricted to having only one metastore per region. A key factor to keep in mind about the metastore is the location of its underlying storage container. This is significant because various catalogs across different business areas may need to access the centrally hosted container. 

To enable Unity Catalog in Azure Databricks, an Azure AD Global Administrator is required initially. The initial Databricks account admin will be the Azure AD Global Administrator, and then additional account admins can be assigned without specific Azure AD roles. The Azure Databricks account must be on the Premium plan. 

Unity Catalog adopts a three-level namespace structure for various types of data assets in the catalog. The below illustrates the structure of the object model.

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-07-object-model-structure.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-07-object-model-structure.png" alt="Unity Catalog Objects Model Structure" width="800" align="center"></a>

*Unity Catalog Objects Model Structure*

<br>

## Cloud Storage

To efficiently handle connections between Databricks and Cloud Storage such as Azure Data Lake Storage, Databricks recommends configuring access to cloud storage exclusively through Unity Catalog.

The following concepts were introduced to manage relationships:

- **Storage credentials** serve as the credential that provides access to the storage account, such as Azure Data Lake Storage. It utilises either an Azure managed identity (recommended) or a service principal.
- **External locations** consist of a reference to a storage credential and a path within the storage account. It provides the authorisation for access to the specified storage path using the storage credential.
- **Managed storage locations** serve as the default storage location for both managed tables and volumes. It represents the locations in the storage account linked to a metastore, catalog, or schema. This allows you to easily secure your data and storage accounts, as it adds another layer of protection. 

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-08-external-data.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-08-external-data.png" alt="External Data - External Locations" width="800" align="center"></a>

*External Data - External Locations* 

<br>

### Access Connector for Azure Databricks

Configuring a managed identity for Unity Catalog in Azure, involves creating an access connector specifically for Azure Databricks. By default, the access connector comes with a system-assigned managed identity, however, you have the option to link a user-assigned managed identity. 

Following this, the managed identity must be given appropriate access to the Storage Account, i.e. Storage Blob Data Contributor/Owner. 

<br>

## Unity Catalog Objects Model

The primary flow of data objects begins from the metastore to tables or volumes. 

All data objects are referenced using the three-tier namespace, the catalog, the schema, and the asset. The following is the format: 

​     `<catalog-name>.<schema-name>.<table/view/volume-name>`     

The below illustrates the hierarchy of each data object. 

<a  href="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-09-object-model-hierarchy.png" target="_blank">
<img src="/images/portfolio/databricks-unity-ultimate-guide/dbx-unity-Introduction-09-object-model-hierarchy.png" alt="Unity Catalog Object Model Hierarchy" width="400" align="center"></a>

*Unity Catalog Object Model Hierarchy*

<br>

Let's explore each data object:

### Metastore

Serves as the top-tier container for metadata, employing a three-level namespace to organize the data. To utilize Unity Catalog, a workspace must be linked to a Unity Catalog metastore. A separate metastore is needed for each region and should be assigned to Databricks workspaces operating in that region.

<br>

### Catalog

This functions as the initial layer in the object hierarchy and three-level namespace. It organises the data assets and contains schemas (databases), tables, views, volumes, models, and functions.

<br>

### Schema (Database)

This forms the second layer of the object hierarchy and three-level namespace. Contains the tables and views held in the schema. Schema is also referred to as databases.

<br>

### Tables

This forms the third layer of the object hierarchy and three-level namespace. This can be Managed or External Tables and contains rows and columns of data. 

- **Managed** tables allow Unity Catalog to manage the data lifecycle and file layout, this is the default table type. Therefore, when managed tables are dropped, the underlying data files are deleted. Data is stored in the root storage location by default, but a specific storage location can be provided at the time of creation. 
- **External** tables, in contrast, do not give Unity Catalog the ability to manage data lifecycle and file layout. Therefore, when external tables are dropped, the underlying data files are not deleted. 

<br>

### Views

This forms the third layer of the object hierarchy and three-level namespace. A read-only object that is derived from one or more tables and views in the metastore. Users can create dynamic views, enabling row- and column-level permissions. 

Views are similar to SQL Views, the data is not persisted in storage. They serve as virtual snapshots that dynamically produce output when executed. This provides a flexible and efficient means to interact with real-time and up-to-date data without the need to persist it. 

<br>

### Volumes (Still in Public Preview as of Jan 2024)

Volumes provide a new approach to load and link external object storage into Unity Catalog. While they store external objects in the data storage directory, they function differently from registered tables. 

Volumes can be managed or external and serve as a conceptual data volume in cloud storage. Unlike tables, volumes offer flexibility to store various file types, including unstructured data like CSVs, PDFs, XML, as well as images, video, audio, and structured or semi-structured data. 

They resemble the traditional storage mounts in Databricks, but Volumes offer enhanced security and controls. The traditional storage mounts were accessible to anyone in the workspace and therefore not very secure. Volumes adhere to the same access and governance policies as schemas and tables, ensuring a higher level of security and control.

<br>

### Functions (Still in Public Preview as of Jan 2024)

This forms the third layer of the object hierarchy and three-level namespace. Registering a custom function to a schema, enables the ability to reuse specific custom logic across the entire environment.

<br>

### Models

This forms the third layer of the object hierarchy and three-level namespace. A model refers to a machine learning model registered in the MLflow Model Registry. Users need specific privileges to create models within the catalogs and schemas.

<br>

## Summary

To sum it up, Unity Catalog from Databricks is a powerful tool for managing and controlling data assets in the Databricks ecosystem. It offers a range of features for discovering, governing, tracking, and securing data, all while maintaining strict access controls and thorough auditing capabilities. 

Unity Catalog provides a reliable and efficient way to handle data assets and is a must-have for any organization that wants to make the most of its data while ensuring compliance and security. 

Considering Databricks' significant investment in Unity Catalog and its continuous new features, it is likely to become the default choice for setting up new Databricks workspaces. Therefore, organizations should consider either establishing new Databricks platforms using Unity Catalog or migrating existing ones to Unity Catalog.

<br><br>

## Reference

https://docs.databricks.com/en/data-governance/unity-catalog/index.html#the-unity-catalog-object-model

https://docs.databricks.com/en/data-governance/index.html

https://docs.databricks.com/en/security/auth-authz/access-control/index.html

https://docs.databricks.com/en/data-governance/unity-catalog/data-lineage.html

https://docs.databricks.com/en/lakehouse/collaboration.html

https://docs.databricks.com/en/data-governance/unity-catalog/audit.html


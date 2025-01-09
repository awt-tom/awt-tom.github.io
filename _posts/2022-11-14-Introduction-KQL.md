---
title: Get started with KQL today!
date: 2022-11-14
categories: [KQL,What is KQL]
tags: [kql,kusto query language,azure data explorer,what is kql,beginner]     # TAG names should always be lowercase
media_subpath: /assets/img/introduction_kql
image:
  path: introduction_kql.png
  width: 100%
  height: 100%
  alt:
---

# What is KQL?

So, maybe you have heard colleagues talk about it, see articles about advanced KQL queries or maybe you are just curious on how to get grip on certain logging data that resides withing your Microsoft environment. There are many reasons why KQL is so interesting. So let’s get started!

## Queries

Before we go into what KQL is, lets start of with the first bits… Queries. 

A query is literally a request for information from a source such as a databases. To be able to make such a request with our query we will need a query language to write the code for this request. Now let’s say we want to ask the database the following question “How many failed sign-ins have been made within the last 7 days”. Of course this will need to be written within a certain query language. This is where KQL comes in!

## KQL
KQL stands for Kusto Query Language. The early version of KQL comes from a project which was created back in early 2014 within the Research & Development center at Microsoft Israel. It was called “Kusto”, here it was in early development. Later in 2019 it was introduces at Microsoft Ignite to be available for general use. With its Kusto Engine V3 (Later in 2021) underneath the hood it has been developed to a more mature product to run your queries as optimized as possible and is currently used by a variety of Microsoft products. 

**Some examples where KQL can be used**

-	Defender for Endpoint
-	Azure Sentinel
-	Azure Resource Graph Explorer
-	Advanced Threat Hunting (Microsoft 365)
-	Logic apps
-	Power BI
-	Azure Data Explorer

The idea of KQL is to be able to explore your data with queries which can be made to recognize anomalies, search for certain patterns or create visual graphs to get a better understanding. A KQL query is a read-only query which collects the data from the source, by the use of a set available operators and filters. Together you will be able to form all the data towards output that will be of use for your specific goal.

In my next blog I will go more into the use of KQL with something new and refreshing called Kusto Detective Agency!

If you cannot wait to start off with using KQL feel free to go to the [Microsoft Learn KQL page](https://learn.microsoft.com/en-us/training/paths/data-analysis-data-explorer-kusto-query-language/)

---
title: The Kusto Detective Agency
date: 2022-11-14
categories: [KQL,Kusto Detective Agency]
tags: [kql,kusto detective agency,kusto query language,]     # TAG names should always be lowercase
media_subpath: /assets/img/kda
image:
  path: kda.png
  width: 100%
  height: 100%
  alt: Import script KDA
---

# Introduction

Recently I started with Kusto Query Language (KQL) to explore the possibility of making lots of data useful or search for specific answers within an environment which contains lots of logs. But as it is quite a task to learn another language I felt it was best to start of with something small. Well, it escalated quickly from there!

You will have multiple options to start from. Might it be through Microsoft learn or going straight up to Advanced Threat hunting. I for myself started with Kusto Detective Agency. This way I can learn KQL, have a good time solving a riddle and earn a cool badge! If you feel like to get to know KQL better before you start off feel free to read my other post about “[What is KQL]( https://azurewithtom.com/categories/what-is-kql/){:target="_blank"}”.

## Kusto Detective

So if you choose to start with Kusto Detective Agency, good! Lets get on with it. 

In the Kusto Detective Agency you get the task to solve multiple riddles. These riddles have a small story so that you will have a real purpose on solving a specific situation. It is not a suprise, but you will be doing this with the use of KQL!

In order to get started go to [Kusto Detective Agency](https://detective.kusto.io/){:target="_blank"}

## Create a free cluster

To create a Kusto Cluster for free head to [Free Kusto Cluster](https://aka.ms/kustofree){:target="_blank"}. To create a cluster you will need either a Microsoft account or an Azure AD Identity in the case you have your own tenant with custom domain.

Fill a suitable name for your cluster and grab yourself a cup of coffee while the cluster is being setup. Once its setup click on **My Cluster** as shown below. 

![Desktop View,img-description](mycluster.jpg)

With this kusto cluster you are able to import the riddle data and be able to build queries to get certain data. You will probably start off by exploring the data and build your way up to this one query which contains the answer to the riddles.

## Import first challenge

So lets add our Cluster URL to Kusto Detective Agency.

Grab the **URI** by copying the url or simply click on the **copy** button. 

![Desktop View,img-description](kusto-cluster-uri.jpg)

Paste the URL into the submit field on the kusto challenge page.

![Desktop View,img-description](kusto-url-check.jpg)

The other field shows that we need to grab a certain score. So lets get the data in our cluster to be able to get the data!

Within the data explorer which contained your cluster uri, click on **Query** which you will find on the menu on the left.
Here we will add the following KQL script in order to create the tables and the files related to the challenge. You can see the files within the Azure Blob url's. 


```
.execute database script <|
// Create table for the data
.create-merge table Onboarding(Score:long)
// Import data
.ingest into table Onboarding ('https://kustodetectiveagency.blob.core.windows.net/onboarding/onboarding.csv.gz') with (ignoreFirstRecord=true)
```
> Only run the KQL script once as this might have impact on the ability to solve the riddle.
{: .prompt-warning }

## Solve our first task
Once the data is loaded you will see a table appear. In my case I called my cluster **kustochallenge** and it contains a database **Onboarding** with a table called **Score**

![Desktop View,img-description](kusto-challenge-table.jpg)

Now let’s get on with it and grab this score by using the following query.

```
Onboarding
| summarize (sum(Score))
```

Let’s break that down.

By saying **Onboarding** in our query I refer to the database which resides in my cluster. So I want to grab data from this database. 

We use a pipe and an [Summarize](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/sum-aggfunction){:target="_blank"} operator to sum up all of the numbers in the **Score** column within the table of the database.

If you have done this correct you will be given a certain number which you can submit on the kusto challenge website.
When the number is correct, you will be given your very first badge, congrats!

![Desktop View,img-description](badge0.jpg)


